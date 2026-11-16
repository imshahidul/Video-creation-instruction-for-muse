# 11 — SFX inventory

Which sound effects exist, what each is used for, timing/mix rules, and
which videos used which cues.

## ⚠️ Audio files are NOT in this repo (API limitation — read this first)

The user ordered the actual SFX audio files to live under an `sfx/` folder
in this repo. **That push is impossible through the GitHub API tools
available to Muse, and it was NOT silently dropped — this section is the
honest record:**

- The snapshot-push guide (`push_files`) supports **UTF-8 text files only**:
  "a snapshot commit creating or updating UTF-8 files, without deletions,
  local Git history, tags, branches, file modes, symlinks, or binary
  contents" — "non-UTF-8 content … reject the whole snapshot".
- `create_or_update_file` takes a text `content` string only ("Do not
  base64-encode it; this server does that before calling the REST API") —
  binary WAV bytes cannot pass through it.
- Verified against the live tool schemas 2026-11-16. No binary push was
  attempted, because the tools cannot carry binary content.

**How to complete it later:** push the audio with plain `git` (clone, copy,
commit, push) from a machine with git access, or upload via the GitHub web
UI in batches. Facts for that push:

- The two CC0 libraries total ~118 MB (433 files: 113 + 320). No single
  file exceeds ~4.3 MB — all under GitHub's 100 MB/file limit, and under
  the ~50 MB caution line. No file was skipped for size.
- **Push ONLY the two CC0 libraries** (sections 1–2 below).
- **NEVER push `sfx-library-yt`** (section 3): 25 WAVs extracted from
  YouTube SFX-demo videos. Rights unclear — local reference only.
- Suggested repo layout when pushing: `sfx/agent-video-editor-library/`
  (113 SFX + 15 music + `catalog.json`) and `sfx/sfx-kit/` (320 sounds +
  `sounds.json` + `catalogue.md` + `GUIDE.md`), preserving each library's
  own folder structure and license files.
- After the audio push, update this file: remove this banner, record the
  commit, and confirm the file counts match the inventory below.

**Exact local paths (authoritative until the audio push happens):**

- Library 1: `~/workspace/brand-beats-videos/audio/agent-video-editor/skills/editing-videos/library/`
- Library 2: `~/workspace/brand-beats-videos/audio/sfx-kit/`
- Library 3 (do NOT push): `~/workspace/brand-beats-videos/audio/sfx-library-yt/`
- Per-video rendered SFX stems (mix outputs, not sources):
  `~/workspace/wholesale-video/full/work/sfx.wav`,
  `~/workspace/wholesale-video/full/work/typing.wav`,
  `~/workspace/wholesale-video/sample/work/sfx.wav`,
  `~/workspace/takbir-video/build/sfx_design.wav`,
  `~/workspace/takbir-video/build/sfx_repo.wav`,
  `~/workspace/takbir-video/build/stage/repo-*.wav` (staged copies).

## 1. agent-video-editor library (CC0, measured)

Source: kmilo93sd/agent-video-editor, cloned at
`~/workspace/brand-beats-videos/audio/agent-video-editor/`.
**113 SFX WAVs (23 MB) + 15 music MP3s (30 MB).** License: CC0 1.0
(`LICENSES.md` in the library dir; per-file origin/license in
`catalog.json`).

- Format: SFX = mono WAV, PCM 16-bit, 48 kHz, normalized to −22 LUFS
  integrated with −1 dBTP ceiling (click/typing sounds un-limited so their
  attack is not squashed; they stay at the peak ceiling and measure lower
  on purpose — they are transients a few tens of ms long). Sounds shorter
  than 0.5 s measured padded with silence to 0.5 s (BS.1770 integrates in
  400 ms blocks). Music = stereo MP3, 192 kbps, 48 kHz, normalized to
  −16 LUFS with −1.5 dBTP ceiling; `clean_loop` field says whether the
  file loops without a click/gap.
- `catalog.json` stores each file's LUFS, true peak, duration, category,
  suggested use, origin, and gain applied. `search.mjs` lists by category
  and prints computed gains: `node library/search.mjs <term> --voice
  <voice_lufs>`.
- Methodology: `skills/editing-videos/references/audio-and-sfx.md` (see
  `03-audio-and-voice.md` for the distilled rules).

### 1a. SFX files (113, sizes in bytes, measured 2026-11-16)

```
alert-soft.wav 68186                  impact-soft-1.wav 50652
ambience-office-busy-45s.wav 4320078  impact-soft-2.wav 54742
ambience-office-hvac-45s.wav 4320078  impact-soft-3.wav 13262
ambience-room-tone-30s.wav 2880078    impact-wood-light.wav 15158
appear.wav 24884                      key-press.wav 3422
back-nav.wav 5932                     keyboard-key-1.wav 24078
beep-short.wav 14478                  keyboard-key-2.wav 21756
bell-ding.wav 59532                   keyboard-typing-1s.wav 96078
book-close.wav 22216                  keyboard-typing-3s.wav 288078
book-open.wav 14580                   keyboard-typing-6s.wav 576078
calculator-keys.wav 115680            keyboard-typing-fast-4s.wav 384078
cash-register-cha-ching.wav 162316    modal-close.wav 14266
check-mark.wav 25502                  modal-open.wav 14266
click-mouse.wav 5500                  mouse-release.wav 6428
click-sharp.wav 2168                  notification-1.wav 26530
click-soft-2.wav 1194                 notification-2.wav 11592
click-soft.wav 8808                   notification-3.wav 11674
clock-tick.wav 27856                  notification-4.wav 9700
coin-clink.wav 56240                  page-turn.wav 73870
coin-drop.wav 53506                   panel-collapse.wav 40204
coins-clink-sequence.wav 135970       panel-expand.wav 38854
coins-handful-1.wav 70830             paper-crumple.wav 110420
coins-handful-2.wav 32546             paper-handle-1.wav 46890
copy-pluck.wav 14620                  paper-handle-2.wav 52464
countdown-beeps-3-2-1.wav 348522      paper-rip.wav 48004
disappear.wav 24884                   paper-shuffle.wav 294174
downlifter-2s.wav 179628              pencil-write.wav 133250
drag-item.wav 73602                   pop-1.wav 18144
drop-item.wav 18144                   pop-2.wav 9634
dry-thud.wav 17396                    purchase-coins.wav 114308
error-1.wav 10110                     question.wav 32000
error-2.wav 13454                     reverse-cymbal-2s.wav 192078
error-3.wav 25346                     riser-long-8s.wav 768078
error-4.wav 15962                     riser-medium-4s.wav 384078
error-buzz-soft.wav 43326             riser-short-2s.wav 192078
glitch-soft-1.wav 30798               scroll.wav 96082
glitch-soft-2.wav 48078               select-1.wav 24098
hover-1.wav 5304                      select-2.wav 23088
hover-2.wav 10668                     send-whoosh-up.wav 43278
                                      slide-1.wav 57754
                                      slide-2.wav 57750
                                      stamp-thud.wav 29308
                                      stinger-calm-pad.wav 441750
                                      stinger-energetic-hit.wav 305596
                                      stinger-fanfare-short.wav 250520
                                      stinger-hit-short.wav 111728
                                      stinger-intro-bells.wav 266104
                                      stinger-outro-soft.wav 454446
                                      stinger-pizzicato-short.wav 127186
                                      stinger-sax-short.wav 167128
                                      stinger-serious-low.wav 500058
                                      stinger-steel-drums-short.wav 149330
                                      stinger-win-brass.wav 211676
                                      stinger-win-piano.wav 245014
                                      stinger-win-strings.wav 282854
                                      stinger-win-vibraphone.wav 270594
                                      success-1.wav 27904
                                      success-2.wav 51824
                                      success-3.wav 30992
                                      success-4.wav 47158
                                      success-bell.wav 153470
                                      success-chime.wav 135004
                                      sweep-long.wav 125504
                                      swell-soft-3s.wav 307278
                                      switch-1.wav 16118
                                      tap.wav 3956
                                      tick-soft.wav 2030
                                      toggle.wav 13176
                                      typing-clicks-3s.wav 272116
                                      whoosh-long-2s.wav 192078
                                      whoosh-medium-1s.wav 96078
                                      whoosh-reverse-1s.wav 105678
                                      whoosh-short.wav 33678
                                      whoosh-soft.wav 67278
```

Suggested uses (from `catalog.json` / `audio-and-sfx.md`): `whoosh-soft`
or `page-turn` + `impact-soft-1` for section title cards (one per card);
`slide-1`/`slide-2` for graphics/cards entering (alternate so it does not
repeat); `pop-1`/`pop-2` when an element appears as the voice names it
(~18–20 dB under voice, not on every element if more than 4); `success-1`
for totals/goals (rarely); `error-1` soft, never looped;
`typing-clicks-3s` / `keyboard-typing-3s` trimmed for animated typing (not
over real recorded typing); `sweep-long` / `downlifter-2s` for closing;
`riser-short-2s` ending on the visual change for builds into a reveal (not
under speech); `ambience-room-tone-30s` ~30 dB under voice where a scene
has no other room sound. Full per-file uses live in `catalog.json` —
consult it, don't guess.

### 1b. Music beds (15, sizes in bytes)

```
music-ambient-piano.mp3 3162860      music-happy-clap-17s.mp3 419948
music-calm-loop.mp3 466885           music-inspiring-orchestral.mp3 2450348
music-contemplation.mp3 2883206      music-lofi-chill-loop.mp3 2334572
music-cozy-acoustic.mp3 3600620      music-lofi-lobby.mp3 2515436
music-emotional-piano-loop.mp3 669356 music-lofi-tea.mp3 4051650
music-energetic-22s.mp3 531116       music-tension-22s.mp3 531116
music-energetic-jazz-funk.mp3 2338604 music-tension-soft.mp3 3062636
music-funky-house.mp3 1649708
```

Known uses: `music-happy-clap-17s.mp3` = wholesale video 1 v1 bed (looped,
2 s crossfades, −18 dB, sidechain-ducked; REMOVED in v3 — no-bed rule);
`music-funky-house` = Muse promo bed (−22 dB under voice, 5.1 dB ducking);
`music-emotional-piano-loop.mp3` = story-video primary bed
(`music-contemplation.mp3` fallback); `music-energetic-22s` = Day 3
English version BGM. All other beds: unused in delivered videos as of
2026-11-16 (do not claim otherwise).

## 2. SFX Kit 1.0.0 by Wyzowl (CC0, sync-pointed)

Source: https://github.com/wyzowl/sfx-kit. Local clone:
`~/workspace/brand-beats-videos/audio/sfx-kit/`. **320 original sounds**
(65 MB of WAVs; 118 MB dir total incl. docs), license CC0-1.0, credit not
required (optional: "SFX Kit by Wyzowl"). Format: WAV, PCM 24-bit, 48 kHz.
Full data: `sounds.json` (per-sound duration, sync point, use/avoid, tags,
variant, level.lufs, tuning, adapt rates). Human catalogue:
`catalogue.md`. Usage guide: `GUIDE.md`. Schema: `sounds.schema.json`.

Category counts (verified 2026-11-16, sum = 320):

| Category | Count | Category | Count |
|---|---|---|---|
| whooshes | 9 | interface | 36 |
| swishes-and-zips | 9 | keyboard | 15 |
| swipes | 6 | writing-and-drawing | 16 |
| reverse-whooshes | 6 | phone | 5 |
| risers-and-fallers | 12 | mechanical | 12 |
| bounce-spin-zoom | 5 | foley | 12 |
| impacts | 12 | everyday-props | 10 |
| cinematic-hits | 8 | notifications | 28 |
| booms-and-bass | 15 | tones | 8 |
| pops | 9 | shimmers | 9 |
| appear-and-vanish | 6 | logo-stings | 14 |
| shape-changes | 8 | celebration | 5 |
| data | 12 | time | 6 |
| digital | 20 | money | 7 |

Per-sound entries (what it sounds like + main use) live in `catalogue.md`
— e.g. `whoosh-fast-hard` 0.25 s for whip pans; `pop-medium-in` 0.06 s for
elements appearing; `keyboard-typing-quick-long` 3.15 s for a full line of
typed text; `tone-step-1..5` rising marimba steps for list items appearing
one by one; `writing-highlighter` for highlighting a key line. Consult the
catalogue per sound; the table above is the map, not the inventory.

**Sync-point placement (the kit's core rule):** start every sound at (the
moment it should meet) MINUS `sync.at`. `sync.at` already points at the
part of the sound that should meet the moment (the hit, the start of a
gesture, a sequence's first event). If a start falls before 0, start at 0
and trim that much off the sound's beginning. If you change a sound's rate,
divide its times by the rate.

**Levels:** every file sits on one loudness scale (`level.lufs` = loudest
150 ms, K-weighted). At 0 dB a medium effect's loudest moment is about
−20.5 LUFS, a few dB under a voiceover at ~−16 LUFS integrated.
`under_voiceover_db` is how far a sound comes down wherever its body
overlaps speech. True-peak ceiling −3 dBTP. Bass-heavy sounds feel louder
than they measure. Tuned sounds are in C major (mostly pentatonic) so they
agree with each other; sounds with `adapt.rate [1, 1]` keep their rate.

**Fitting:** `span_seconds` is the length of moment a sound fits at rate 1;
rate = `span_seconds ÷ moment length`, within `adapt.rate`. A sound that
runs with an action can lose its end; a build ending on its sync point can
lose its start; cut just before a part's time to drop a later part. Files
start/end on silence — a mid-sound cut needs a short fade (10–50 ms, or
300 ms+ for a long tail).

## 3. sfx-library-yt — DO NOT PUSH (25 WAVs, 6.2 MB)

`~/workspace/brand-beats-videos/audio/sfx-library-yt/` — sounds EXTRACTED
from the three YouTube SFX-demo Shorts studied for the style guide (YT1
3BTXSTK5KXo, YT2 eCF_1QYhwQQ, YT3 rWczAMtK32c). Manifest:
`MANIFEST.md`, extraction report: `_extract_report.json`. These are
reference/demo-pack sounds belonging to their creators — **rights unclear,
local reference only, never redistribute, never push to this repo.**

Files: `yt1_basscrack`, `yt1_camera-flash`, `yt1_cash-register`,
`yt1_confirm-tap`, `yt1_digital-click-2`, `yt1_drums-of-war`,
`yt1_grand-hit`, `yt1_hit-drum_deep-impact`, `yt1_universfield-impact`,
`yt2_apple-notification`, `yt2_camera-flash`, `yt2_discord-join`,
`yt2_discord-leave`, `yt2_game-menu`, `yt2_gear-turn`, `yt2_happy`,
`yt2_paper-fold`, `yt2_pop`, `yt2_whoosh-fire-transition`, `yt3_bruhhh`,
`yt3_dark-gravel-hit`, `yt3_error`, `yt3_gone-fast_airy-slice`,
`yt3_multiple-shuttle`, `yt3_snapshot-woosh` (all `.wav`).

## 4. Timing and mix rules (apply to every cue)

1. **Audibility vs the voice** (hard): every cue's peak must clear the VOICE
   at the same second, or sit in a real speech gap. A music-relative margin
   proves nothing. Record peak/RMS of cue and voice per second; report the
   buried count at delivery. Full rule: `03-audio-and-voice.md`.
2. **Denoise-only-source:** SFX are mixed AFTER denoising, never through
   the denoiser. Denoise ONLY the source audio FIRST; never denoise a
   finished mix; never chain denoisers. Full rule: `03-audio-and-voice.md`.
3. **Placement:** transient 2–4 frames BEFORE the visual change (library
   rule); SFX Kit sounds use their `sync.at` offsets; wholesale builds
   place each cue in the QUIETEST 300 ms window within ±0.75 s of its word;
   pops never before the card appears. Trim silence at the start of the
   file first.
4. **Gains computed, not guessed:**
   `gain = 10^((voice_lufs − under_voice − sound_lufs)/20)`, capped at 1.
   Defaults: SFX 15 dB under voice (range 12–24), music ~20 dB, ambience
   ~30 dB. If gain > 1, pick another sound. Wholesale practice: clicks
   −3 dB, pops 0 dB, typing −9/−10 dB (measured per build, verified 0
   buried — these are build measurements, not defaults to copy blindly).
5. **Limits:** SFX on beats only (card in, stat reveal, section change,
   CTA); NO whoosh on every continuity cut; same sound max 3× in a row;
   never louder than voice or on a key word; no sounds over real recorded
   sounds that already do the job; no long tails; no risers fighting the
   voice. Typing SFX trimmed to grapheme-count/cps, only for
   numbers/addresses actually spoken.
6. **Mix mechanics:** pre-convert EVERY input to stereo 48 kHz WAV before
   `amix` (else mono collapse); apad the voice branch for sidechain (else
   truncation); aresample to 48000 after loudnorm (else 192 kHz); mono
   sources use `pan=stereo|c0=c0|c1=c0` (never `c1=c1` — silent right
   channel); float premaster (s16 clips at cue+voice coincidences); numpy
   SFX mix when ffmpeg cue graphs hang.
7. **Story videos:** SFX follow the SPOKEN WORDS; story-world sounds tied
   to the spoken word, never generic UI pops; soft whoosh only on major
   section changes. See `08-story-videos.md`.

## 5. Which videos used which cues

| Video | Cues | Detail |
|---|---|---|
| Wholesale video 1 v1/v3 (KM jackets) | 27× `keyboard-key-2` clicks (−3 dB, raised from sample's −8 dB) + 11× `pop-1` pops (0 dB) + 6 typing spans (−10 dB, fast-typing loop trimmed to grapheme-count/cps) | 38 cues, 0 buried (v3 margins +1.0 to +45.9 dB). Whooshes DROPPED (sample evidence: inaudible under dense speech). Typing 15.9–19.1 dB under voice RMS per span. Sample v1: 7/8 cues buried (pre-fix). |
| Wholesale video 2 (KM jeans) | 60 clicks + 29 pops + 5 typing spans (−9 dB) | 89 cues, 0 buried (tightest +1.7 dB). Typing stems −35 dBFS RMS, 6–10 dB below voice, silent outside spans. numpy mix. |
| Muse promo (2026-11-12) | 14 SFX from wyzowl/sfx-kit | Pops on card entrances, soft whooshes on major changes ONLY, shimmers on the ১ বিলিয়ন / ৩১ বিলিয়ন reveals, riser + sting on the end card. Bed: funky-house −22 dB, 5.1 dB ducking. |
| Takbir v5 / design mix | 399 events: 72 transition whooshes (peak on dissolve midpoint) + 297 ticks at text reveals + 30 beat accents; repo mix used `whoosh-soft`, `slide-1`, `success-1` (+ `calculator-keys`, `bell-ding` measured) | ALL REJECTED by the user; work DROPPED 2026-11-13. Calculator keys max −24 dB vs voice −3 dB; bell −26 dB vs voice −6.9 dB (the audibility-rule proof). Do not resume without explicit order. |
| Sales video 1 sample | 9 SFX | None buried. (Per-cue identities not recorded in the sample note — gap.) |
| Sales video 1 v2 (blocked) | 22 SFX kept | Audio final −15.62 LUFS / −1.78 dBTP. (Per-cue identities not recorded — gap.) |
| Sales video 2 v1 | 10 SFX kept / 6 dropped | 0 buried. (Per-cue identities not recorded — gap.) |
| Sales video 3 v1 (blocked) | 37/37 SFX | 0 buried. (Per-cue identities not recorded — gap.) |
| Interview sample v2 | (SFX present; mono pan bug found here) | `pan=stereo\|c0=c0\|c1=c1` on mono → silent right channel. Fix: `c1=c0`. |
| Day 3 English | 20% clicks buried | Honest gap disclosed at delivery. |

**Gap note:** sales-video build notes record cue COUNTS and buried counts
but not per-cue file identities. Future builds must record which library
file each cue used, so this table stays exact. When a new SFX is added to
either library or a new video uses cues, update this file (and the
`11-sfx-inventory.md` counts) in the same change as the repo update.
