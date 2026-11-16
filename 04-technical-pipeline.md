# 04 — Technical pipeline

## Remotion (pinned)

- **Remotion 4.0.200, React 18.3.1, @remotion/transitions.** Project lives
  at `~/workspace/remotion/`. Do not upgrade without re-checking the
  port-probe patch.
- **Port-probe patch is mandatory on this VM:** the sandbox fake-accepts TCP
  connects to wildcard addresses (`::`/`0.0.0.0` report CONNECTED on closed
  ports) while 127.0.0.1 correctly refuses — Remotion's port probe reported
  all ports 3000–3100 busy and the first render failed with "No available
  ports found". Fix: `~/workspace/remotion/scripts/patch-remotion-ports.js`
  strips wildcard hosts from the probe in
  `@remotion/renderer/dist/port-config.js`, wired as `postinstall`, pinned
  to renderer 4.0.200. Chrome Headless Shell lives in
  `node_modules/.remotion/` (re-run `npx remotion browser ensure` if
  node_modules is wiped).
- **Concurrency 1 is MANDATORY for video-containing compositions**
  (~3 min/600 frames). Concurrency 2 + OffthreadVideo fails with
  ERR_INSUFFICIENT_RESOURCES (~frame 113). Concurrency 2 works at
  1080×1440 for non-video comps; drop to 1 if OOM.
- **TMPDIR on disk is MANDATORY:** `TMPDIR=~/workspace/.tmp-remotion`.
  The 512 MB /tmp tmpfs fills during frame extraction → ENOSPC /
  ERR_INSUFFICIENT_RESOURCES.
- **Single full renders crash Chrome ~frame 1377.** Render in segments
  (1962 frames each, fresh browser per segment, ~13–22 min each), verify
  exact frame counts, concatenate losslessly (`-c copy`, video only), mux
  the mixed audio as the only audio. Run segments INDIVIDUALLY, never as
  one long chain (a 4-segment chain was SIGTERM-killed at ~40 min by the
  background exec cap after 2 segments; solo re-launches passed).
- **Chromium SIGTRAP (exit 133) — 2026-11-16:** plain launches die. Add
  `--no-enable-multiprocess-on-linux` to EVERY Remotion render/still
  invocation (prefer direct binary over npx). Identified 2026-11-16;
  end-to-end proof pending environment recovery.
- **OffthreadVideo `endAt`:** `endAt` = last frame renders BLACK at the
  boundary (frames 359/599 were 99% black) — use
  `endAt = from + duration` (one past the last needed frame).
- **`<Sequence>` escape bug:** `<Sequence>` renders an absolutely-positioned
  div — every div wrapping a `<Sequence>`/`<OffthreadVideo>` MUST be
  positioned (`position: relative` or absolute), or the video escapes to
  the nearest positioned ancestor, covers text, and its card border
  vanishes. Always check footage-card containment on QA frames.
- **Full-frame slide + opacity fade = dissolve ghosting** (speaker ghosted
  through B-roll) — full-frame slides must be fully opaque; fade only for
  cards over backgrounds.
- **Bangla renders correctly in headless Chrome** via `~/.fonts/bangla-test/`
  + fontconfig. Hind Siliguri Bold for captions/headlines.
- **Caption-ghost fix:** strictly increasing caption starts, index keys,
  per-phrase remount.
- **Type-on cards:** grapheme-safe via Node `Intl.Segmenter`, blinking
  cursor, typing SFX; cards complete just before/while the words are
  spoken. Verify grapheme counts against the sample.
- **Split-card framing:** full title + full face + captions cannot fit in a
  590 px card — the split shows only the strip; full title stays in
  full-frame speaker beats.
- Render command shape: `npx remotion render <Comp> out/x.mp4` with
  concurrency 1 + TMPDIR on disk + the multiprocess flag (2026-11-16).

## Concat / PTS checks

- Concatenate segments losslessly (`-c copy`); drop segments' silent audio
  tracks; mux `mixed.wav` as the only audio.
- **PTS check in PRESENTATION order** (`-show_frames`), never packet order:
  packets are in DECODE order and B-frames make packet PTS non-monotonic
  (a packet-order check once flagged 3830 false "regressions").
- Boundary steps of +0.084 s at segment joins are NORMAL (1 frame + the
  +0.05 s container tail step) — verified identical in video 1's silent
  concat. Max A/V drift 0.15 s at the fade-out tail is imperceptible,
  within the 0.28 s caption bridge.
- Verify: exact frame counts per segment, 0 non-increasing presentation
  steps, only the expected boundary steps.
- **Segment-concat drift: strip the silent audio BEFORE concat
  (2026-11-16).** Each Remotion render part carries a SILENT AAC audio
  track ~0.059 s LONGER than its video track; when parts are concatenated,
  the demuxer offsets each subsequent part, producing cumulative video
  drift (+0.367 s measured on sales-video-1 v2's first mux). Mapping only
  the video stream does NOT fix it. FIX: strip the silent audio from every
  part before concat (frames bit-identical), re-concat, re-mux. VERIFY:
  the final file must show perfectly uniform 1/30 s frame steps (first pts
  0.0, last pts = (N-1)/30) with the frame count identical to the sum of
  the parts. Evidence:
  `~/workspace/sales-video-1/work/qa_v2/drift_before_fix_frames.json`.

## Bangla caption shaping (hard rule)

- **NEVER ffmpeg libass / subtitles filter for Bengali** — it breaks shaping
  (matras/reph displaced) for EVERY font tested. Two independent proofs:
  the Muse promo (broken Bangla was libass, not the font) and wholesale
  video 2.
- Correct routes: (a) Remotion/Chrome rendering with Hind Siliguri Bold;
  (b) captions rendered as PNGs with PIL + libraqm (`Layout.RAQM`) and
  overlaid as a video stream. Verify conjuncts on final frames
  (সবচেয়ে, বিলিয়ন, সর্বোচ্চ, উদ্দেশ্য, ক্ষ/জ্ঞ/স্ত/স্ক্র).
- Caption systems in use: last-3-words window, 58 px, gold `#FFD600`
  keywords + animated highlight bar, 0.28 s bridge hold, bottom scrim
  (wholesale); word-by-word karaoke; kinetic headlines; subtitle pill with
  current-word accent (long-form option).

## Transcription / alignment

- **faster-whisper needs ndarray input.** large-v3 int8 with 10 s windows
  avoids DTW drift.
- Wholesale video 1: Google Speech (bn-BD + bn-IN, 12 s chunks + 4 s
  retries + denoised-audio retries) governs SPELLINGS; Whisper base
  timings (3 passes, 272 anchors) govern WORD TIMES; chunk-window
  distribution with anchor warping where ≥3 anchors span ≥1 s, else even
  spread. 10 overlap-duplicate hearings deleted with asserted logs.
- Wholesale video 2: faster-whisper base for timings + Google Speech
  (bn-BD, 64 chunks) for spellings; faster-whisper "small" failed outright
  on that audio.
- Sales video 3: 31 chunks, midpoint assignment + debris drop + gap-fill +
  stretched-token recovery + overlap-dedup; 657 words, 75 phrases.
- Timing quality varies: phrase boundaries are reliable (chunk-window
  edges); word times inside windows without Whisper anchors are
  interpolated approximations — say so honestly. Approximate-timing regions
  must be flagged in the build note.
- Story videos: phrase timing via silencedetect + RMS in story order —
  NEVER Whisper word timings for story text accumulation.
- Word timings must be measured from the REAL audio, never a global
  chars/sec rate. (One historical fallback: whisper timings unusable for a
  promo, words evenly distributed within known phrase chunks — a fallback,
  not the method.)
- Whisper hallucinates on non-speech audio (invented a YouTube outro phrase
  spanning two SFX bursts in an SFX-demo video). Reject low-probability
  candidates inside hallucinated segments.

## ffmpeg picture chains

### Enhancement chain (sales videos, frame-tested)

```
hqdn3d=3:3:4:4 → crop → scale 1080:1350 lanczos → cas=0.6
→ eq=contrast=1.06:saturation=1.12:brightness=0.01
```
CRF 16. Order matters: denoise → crop/scale → sharpen → grade. Denoising
first avoids sharpening noise; sharpening after scaling avoids halos.
Ceiling: `cas=0.8` at most; do NOT switch to `unsharp` ≥1.0 (halos + noise,
proven in the strong variant). Do NOT add a second sharpen pass in Remotion
(double sharpening = halos). `nlmeans` is much slower with no visible gain
at 29.5 Mbps source bitrate. `deblock`/`deband` unnecessary at that bitrate.
No film grain (sales video should look clean, not filmic).

### Validated grades (do not switch without viewed-frame evidence)

- **Video 1 E2** (sales): shadows AND midtones rise vs RAW at every
  timestamp (t11 p10 12 → 32, meanY 89.2 → 116.2), highlights hold (0.14%
  px >240, 0.00% >250 on the hottest frame), skin natural, cream weave
  preserved at 100% zoom. See
  `~/workspace/sales-video-1/work/grade_v2/GRADE_V2_VALIDATED.md`.
- **Video 2 G4** (sales): the curves chain —
  `curves=r='0/0 0.25/0.33 0.5/0.56 0.75/0.76 1/0.97':g='0/0 0.25/0.31 0.5/0.54 0.75/0.76 1/0.98':b='0/0 0.25/0.28 0.5/0.52 0.75/0.75 1/1',eq=saturation=1.30`
  — also the prescribed starting point for video 3 (not E2: E2 overshoots
  on bright cream frames; not filmic: flat/desaturated). Tuning: if dark
  frames read dim, lift ONLY the 0.25 curve points slightly (G4→G4+), never
  add eq brightness (re-pushes highlights — proven in G3→G4).
- **Video 3 V2** (sales, later FAILED re-validation — see below):
  `eq=contrast=1.12:saturation=1.35:brightness=0.03` + warm colorbalance
  `rs=0.07:gs=0:bs=-0.07`. The 2026-11-16 grade research found V3V2 fails
  the brightness standard on new frames (darker than raw on t05/t270, clips
  cream on t60) — do NOT ship V3V2 as-is; use G4. Evidence in
  `~/workspace/sales-video-chain/grade-research/REPORT.md`.
- **Wholesale video 1:** `eq=brightness=0.02:contrast=1.06:saturation=1.15,
  colorbalance=rs=0.04:gs=0.01:bs=-0.05, unsharp=5:5:0.6:5:5:0.0`,
  reframe crop 864×1080 at x=320 → 1080×1350, graded footage CRF 18.
- **Wholesale video 2:** `crop=864:1080:320:0,
  eq=brightness=0.0:contrast=1.08:saturation=1.22,
  colorbalance=rs=0.04:gs=0.01:bs=-0.06, unsharp=5:5:0.7:5:5:0.0,
  scale=1080:1350:flags=bicubic, fps=30, format=yuv420p`, CRF 18.
- **Crop position is per-segment:** the speaker sits right-of-centre and
  garments drift right; a centre crop cuts the vest, a further-right crop
  cuts the speaker. Choose CROP_X per segment from viewed frames (sales
  video 1 used x=560 for one segment, x=480–500 elsewhere; video 3 used
  x=500; wholesale used x=320).
- Grade rules: grade must be VISIBLE side-by-side (brighter, garments pop,
  warm pleasing shop look); skin natural; protect highlights (cream
  garments near clipping — do NOT push contrast past ~1.08 in the eq-only
  chain); no clipped highlights, no crushed blacks, no extra lossy passes
  (single-pipeline encode: denoise/crop/scale/grade in ONE pass, CRF 16).

### Grade research verdict: NO adoption (2026-11-16)

20 repos checked, 10 render-tested, nothing adopted. color-fx
(github.com/tomastimelock/color-fx) is archived/closed. Free LUTs push the
wrong way: Kodak 2383-style (dense blacks, cool shadows) re-crushes the
shop; Portra 400-style softens contrast and risks washing cream garments;
teal/orange + moody packs are the wrong palette. Filmic/Hable curve: best
highlight guard but flat/desaturated (chroma at or below raw on 7/10
frames). slay Portrait LUT: no brightness lift. color-grade-ai: darkens +
  crushes (its own analysis judged frames "overexposed" and targeted cool
  shifts — the opposite of the goals). Histogram-matching is circular (E2/G4
  ARE the target look). Full evidence:
  `~/workspace/sales-video-chain/grade-research/REPORT.md` and
  `~/workspace/sales-video-1/work/grade_v2/GITHUB_GRADING_RESEARCH.md`.

### AI upscalers: honestly ruled out on this VM

- Real-ESRGAN: ncnn-vulkan build needs a GPU (none here); Python route needs
  PyTorch + basicsr (not installed); published CPU figures put the full
  158 s video at 16+ hours to days, with flicker risk and invented texture
  on fabric weave. RealBasicVSR: 2021 CUDA stack, ~20 GB VRAM quoted.
  CodeFormer/GFPGAN: face-only, GPU, not applicable (the selling subject is
  fabric). Diffusion/heavy video models: 8–24 GB+ VRAM. Full record:
  `~/workspace/sales-video-1/work/enhance/ENHANCEMENT_RESEARCH.md`.
- Honest limits: no true detail can be added (864→1080 px is interpolation);
  out-of-focus softness and motion blur stay; blown highlights stay blown;
  the 4:5 crop discards ~55% of horizontal pixels; delivery compression
  will soften the result again (master high-bitrate).

## Zooms / inserts

- Zooms: phrase-class based keys — feature phrases (jacket/quality/material/
  embroidery/stitching/wash/front/back/color/design) punch to 1.14 with
  garment focal ~y=950; talk phrases 1.05; type-on phrases ease 1.04; slow
  drift keys inside long caption gaps so nothing ever sits static
  (wholesale video 1: 62 keys; video 2: ~149 keys + drift keys in gaps
  >2.5 s).
- Detail inserts: scale 2.0, hold 3.5–4.0 s, origins verified on cropped
  source frames, non-overlapping (wholesale video 2: 11 inserts).
- Sales B-roll: ZOOMED IN on fabric texture (weave/jacquard/embroidery/
  buttons); full view briefly for context only. Item-match rule still
  applies — B-roll colours that do not exactly match footage garments are
  used ONLY at generic/quality moments, NEVER during color-naming.

## QA tooling

- **ffmpeg QA extractions must pass `-y`** — re-extracting over existing
  files without `-y` hangs forever on the overwrite prompt (killed a QA
  session). Always `-y` + single-pass extraction in QA scripts.
- blackdetect (d=0.2) + freezedetect (n=−50 dB, d=1.0) over the full
  duration: 0 hits expected (the fade-out tail is gradual, not a black
  segment).
- 2 fps sweep: ALL frames viewed (wholesale video 1: 523 frames / 22
  sheets; video 2: 784 frames / 33 sheets). 10 fps dense: all card/callout/
  type-on spans + head + tail, ALL sheets viewed. Per-phrase caption crops
  vs the transcript (56/56, 149/149). Per-card frames (17/17, 29/29).
- QA script traps: ffmpeg inside `while read` eats stdin (rewrite that step
  in Python with stdin DEVNULL); a piped `QA_EXIT:0` may be `tail`'s exit
  code, not the script's — always check artifacts, not the piped exit code.
- A/V sync: audio-envelope correlation after cuts at multiple boundaries
  (mapped >> naive at every boundary). Sample-level correlation is degraded
  by DFN phase changes but still peaks at the mapped position; envelope
  proof is conclusive.
- 5-point preview QA checklist (1DKM adoption): text on the right word; no
  text/picture off-screen; subtitles readable; sound/music not burying the
  voice; no scene empty or monotonous. Fix ONLY flagged scenes.
- **LIVE VERIFICATION:** the parent views actual rendered frames/clips
  before delivery — never deliver on settings/descriptions alone.
- **Faststart probe false-fail (2026-11-16).** A faststart check that reads
  only the first 200 KB false-fails correct files when the moov atom is
  larger (sales-video-3 v1's moov is 317 KB). FIX: widen the probe window
  to 2 MB (qa_v3.py).

## Environment limits (this VM)

- CPU: 4 cores visible, cell limited to **1.5 shared CPUs** (throttled).
  Measured ffmpeg throughput ~2.5 fps at 1080×1350 (x264 medium).
- RAM: 7.7 GiB total, often only ~1.4 GiB available. No headroom for large
  untiled neural inference.
- **GPU: NONE.** No nvidia-smi, no /dev/dri, no Vulkan. Anything needing
  CUDA or Vulkan cannot run. No torch, no OpenCV installed; onnxruntime
  1.31.1 CPU-only; Python 3.12.3; ffmpeg 8.1.2.
- **/tmp is a 512 MB tmpfs.** Remotion renders, flutter tests, and pip
  installs must use TMPDIR on disk (`~/workspace/.tmp-remotion` etc.).
- **Deploy image Python ≠ VM Python:** the api image runs python3 = 3.11;
  this VM runs 3.12.3. Verify every venv pin with
  `pip install --dry-run --python-version 3.11 --only-binary=:all:` before
  changing pins; a local venv install proves nothing about the image.
  Proven pins: rembg==2.0.86 + onnxruntime==1.31.1 + scipy==1.17.1.
  (Plain `rembg` ships NO onnxruntime backend; scipy 1.18.x requires
  >=3.12.)
- **Sandbox DNS lies about external hosts:** DNS returns SYNTHETIC RESERVED
  addresses (e.g. `api.brandbeats.agency` → 198.18.193.157 instead of the
  real 13.239.253.233). SSRF guards reject 198.18.0.0/15, so server-side
  fetches of public URLs fail in this sandbox even when the code is right
  — live confirmation must happen post-deploy. `/etc/hosts` and
  `/etc/resolv.conf` are read-only mounts. rembg models live in
  `~/.rembg/models/` (not `~/.u2net`); local API boots need `BGREM_SCRIPT`
  set.
- **Filesystem taint fault (2026-11-16 ~12:50 +06, unresolved at time of
  writing):** any exec session that READS a file under `/home/hatch`
  predating ~06:50 UTC loses write permission (EPERM, 0-byte files).
  Marker: `user.hatch_tainted=1` xattr; `cp` cannot launder. Recovery
  requires VM/runtime restart or taint-state refresh. Recovery test: in ONE
  exec session, read a pre-06:50-UTC file, then write a probe — success
  (non-zero bytes) = recovered. This fault likely caused a background save
  of MEMORY.md to become 0 bytes.
- **Dead apt mirror after VM replacement:** `apt-get update` hung 8+ min on
  `mirror.cogentco.com` while `azure.archive.ubuntu.com` answers in ~1 s.
  Fix: remove cogentco from `/etc/apt/sources.list.d/ubuntu.sources`, keep
  azure.archive only. Always curl-test mirrors before a long apt run.
- **npm ci is fragile:** a killed/concurrent `npm ci` leaves node_modules
  half-installed; the `@prisma/engines` postinstall aborts with ECONNRESET.
  Never run two `npm ci`/builds concurrently.
- **Local smoke-test ports are shared:** the main chat runs dev servers on
  :3000/:3100/:3101 — always `ss -tlnp` first and use a free port (3190+).
  Kill leftover servers by exact PID only. NEVER `pkill -f` (matches the
  exec shell's own command line and SIGTERMs it).
- **Pre-tarball symlink sweep:** local builds can create ABSOLUTE symlinks
  at app roots that ship in tarballs and break remote builds. Before EVERY
  tarball build, `find . -type l -not -path '*/node_modules/*'` must be
  empty. Also exclude `*.tsbuildinfo`.
