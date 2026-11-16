# 03 — Audio and voice

## Master standard

- **Target: −14 LUFS integrated, true peak ≤ −1 dBTP** (build standard for
  all videos). Two-pass loudnorm: `I=-14, TP=-2, LRA=7, dynamic`
  (TP=−2 in the loudnorm stage leaves headroom for the AAC encode; see the
  true-peak notes below).
- **True-peak ceiling is prioritized over hitting −14 exactly.** Delivered
  files run −15.4 to −15.6 LUFS with the ceiling held — accept and disclose
  the LUFS, never breach the ceiling to chase the number.
- AAC 48 kHz stereo 192 kbps, faststart. Force 48 kHz stereo AAC output —
  a loudnorm chain once upsampled samples to 96 kHz AAC unnoticed.
- Verify on the FINAL file (ffprobe + ebur128), not only on the WAV master.
  AAC inter-sample overshoot on sharp click transients can add ~+1.75 dBTP
  over the WAV master (wholesale video 1 v1: WAV −1.87 dBTP, AAC +1.75
  dBTP). The fix that worked (wholesale video 2): rebuild with a lower
  limiter (0.70 instead of 0.79) — WAV −14.30/−3.10 → final file
  −14.31 LUFS / −1.97 dBTP, at a cost of 0.23 LU.

## The cue-audibility rule (hard, measured twice)

**Every sound cue must clear the VOICE at the same second, or sit in a real
speech gap. A margin measured against the music proves nothing.**

- Proven failure (Takbir v5): cues passed at ≥6 dB over the ducked music,
  but the voice sits 11–20 dB over the music, so cues on speech onsets were
  19–21 dB under the voice peaks and inaudible (calculator keys max −24 dB
  vs voice max −3 dB; bell max −26 dB vs voice −6.9 dB). The user rightly
  heard "no graph/text sounds".
- Same failure in the wholesale sample v1: 7/8 cues buried by the strict
  peak-vs-voice rule (1 pop cleared).
- Method: record peak and RMS of the cue AND of the voice in the same
  second; a cue is buried when its peak sits below the voice peak at that
  second. Record the buried count for the whole video with per-cue numbers
  beside each cue time. Re-measure every cue after any gain or timing move.
- Placement: put a cue in a real speech gap when the voice would bury it;
  move it to the nearest gap instead of raising music ducking to hide the
  clash. Raise cue gain only when the cue must stay on a spoken beat and
  the raised peak still clears the voice peak without clipping. Never lower
  the voice as a quiet fix for a buried cue. Never report a cue as audible
  from a music-only margin; never deliver with a buried cue left unreported.
- Placement refinement (wholesale builds): place each cue in the QUIETEST
  300 ms window within ±0.75 s of its word; pops never before the card
  appears. Wholesale video 1 v3: 0/38 buried (margins +1.0 to +45.9 dB).
  Wholesale video 2: 0/89 buried (tightest: pop @4.74 s, +1.7 dB margin —
  a sample-exact cue, approved).
- Alternative when a spoken beat leaves no audible room: use a softer cue
  or a visual cue, or drop a cue that adds no meaning when the voice
  already carries the moment.
- Full skill: `~/workspace/custom-skills/video_sound_cue_audibility/SKILL.md`.

## Denoise

### Standing rule: denoise ONLY the source, FIRST

- Denoise ONLY the source video's own audio FIRST. SFX are mixed AFTER,
  never through the denoiser. Never denoise a finished mix. Never chain
  denoisers. No `--pf` unless the user asks.
- The user is the final ear: Muse cannot hear. Numbers + spectrograms say
  what changed; only the user can judge robotic/phasey artifacts, swallowed
  consonants, or over-gating. Say so honestly at delivery.

### DeepFilterNet (approved 2026-11-15) — the method

- Binary: `~/workspace/wholesale-video/full/work/denoise/tools/deep-filter-0.5.6`
  (v0.5.6, DeepFilterNet3 model embedded, 36,417,296 bytes, static Rust
  binary, MIT + Apache-2.0). No Python/torch needed.
- Command: `deep-filter-0.5.6 -D -o <outdir> <input-48k-mono.wav>`
  `-D` compensates STFT+lookahead delay (measured A/V lag 0 ms). Input must
  be 48 kHz WAV. Runtime ~9.5 s per 22 s excerpt including model load
  (~2 min for a full 261 s file).
- Apply to the FULL good-channel voice FIRST, before pause cutting. DFN
  output is ~30 ms shorter at the TAIL only (1,440 samples) — absorbed by
  the mix fade-out. Verify alignment by envelope cross-correlation (lag
  0 ms, corr 0.997–0.999).
- Do NOT highpass before DFN unless tested: DFN handles rumble itself; the
  sample runs used NO highpass. Do NOT chain DFN + anlmdn/afftdn (stacking
  erodes consonants — proven harmful). `--pf` (post-filter) is one flag
  away for even quieter gaps (raw floor −107 dBFS = digital silence) but
  stays the user's choice, not the default — if gaps sound unnaturally
  "dead", fall back to default or mix original back with `-a`.
- Measured (22.2 s excerpt, same as the anlmdn sample): source floor
  −43.8 dBFS → DFN default −87.7, DFN+pf −107.0; speech −10.5 → −11.6/−11.7;
  0% clipped; spectrograms show dark/silent gaps with speech harmonics
  intact, no musical-noise islands. Delivered-sample floors: DFN −83.6
  dBFS (+24.8 dB vs anlmdn), pf −103.4 (+44.6 dB). AAC encode raises the
  raw-WAV floor ~4 dB (codec noise floor).
- "Possible clipping detected (1.000)" warnings during the run are internal
  float overshoot — output WAVs peak at −1.01 dBFS with 0% clipped samples.
- DFN preserves real transients in gaps (correct) and cannot remove noise
  riding UNDER speech. On a pre-denoised source (wholesale video 2, which
  the user had already denoised himself), the measured effect is subtle:
  gaps gated to silence, speech unchanged within 0.3 dB.
- Full record: `~/workspace/wholesale-video/full/work/denoise/GITHUB_DENOISE_RESEARCH.md`.

### Rejected denoise methods (do not reuse without new evidence)

- **ffmpeg `afftdn` / `anlmdn` chains — REJECTED by the user as "very bad"**
  (2026-11-15 12:26). afftdn nr=8 cut only 4.0 dB + distorted speech
  (LSD 10.7); stronger afftdn worse; afftdn-after-anlmdn harmful. anlmdn
  floor −44.6 → −58.8 dBFS (14.2 dB) on the excerpt — still rejected.
- **ClearerVoice-Studio FRCRN_SE_16K — TESTED, NOT RECOMMENDED.** 16 kHz
  only, 9.2× real-time on CPU (~40 min for 261 s), floor −71.7 dBFS
  (16 dB worse than DFN), residual wash visible in gaps. MossFormer2_SE_48K
  not run (heavier; FRCRN already loses on suppression and 20× on speed).
- **facebookresearch/denoiser (Demucs dns64) — REJECTED on license**
  (CC-BY-NC 4.0, non-commercial) + stale + 16 kHz only. Do not use for
  Brand Beats deliverables.
- **resemble-ai/resemble-enhance — REJECTED.** Generative 2-stage
  (hallucination risk on Bangla words), ~1 GB models, buggy/slow CPU path.
- **UVR / MDX-Net, SepFormer / SpeechBrain** — wrong tools (music
  separation / speaker separation, not speech enhancement).
- **noisereduce (spectral gating)** — same DSP class as afftdn, which
  already failed; not tested, no reason to expect a leap.

### Channel selection

- Check channels before extracting: in all three sales sources and both
  wholesale sources, the LEFT channel was the good/close mic (6–7 dB hotter,
  higher speech-band share); the right was distant/ambient. Verify per file
  with volumedetect + per-window levels + speech-band share — never assume.
  Use L only, everywhere, once verified.

## Voices

- **Bangla voice for ALL videos: ElevenLabs 'Rahat - Narrator'.** The user
  provides the audio files (ElevenLabs account work itself stays paused).
  Supersedes Poulomi (2026-11-12 22:50). Earlier: Helio avocado_v2:MAI_03
  at speed 85 was the Dulha-accepted combo; both speed-100 attempts were
  rejected — historical only.
- **English versions: Melody voice.** (Day 3 English, price-anchoring
  English, seal English all Melody.)
- **Voice cloning:** the user ordered cloning from his samples ("তোমার কাছে
  অডিও স্যাম্পল আছে। ক্লোন করো", 2026-11-14). 7 ElevenLabs 'Rahat -
  Narrator' mp3s exist in `~/workspace/user/files/`. Status of any cloning
  work is NOT recorded as complete — do not claim it exists.
- **Voice-script rules** (from the 1DKM adoption, 2026-11-14): numbers
  always in WORDS in voice scripts, never digits; words the TTS cannot
  pronounce are excluded from the script; for mixed Bangla+English, the
  voice file writes English words in Bangla letters (so TTS pronounces
  them right) while the subtitle file keeps English in English, with EQUAL
  word count per line.
- **Voice-first:** voice before video always; word timings to fractions of
  a second; scene plan shown/approved before building.
- Voice processing (promo/interview): light compression + high-pass ~80 Hz;
  voice sits 10+ dB over the ducked bed at all times.
- Muse cannot hear: voice quality itself CANNOT be verified by Muse — the
  user is the final ear on every voice decision.

## Music beds (by video family)

- **Wholesale/sales videos: NO background music.** Voice + SFX only.
  Bed-absence is VERIFIED, not assumed: quietest-100 ms-window floor mean
  −67.3 dBFS (mixed, no bed) vs −42.9 dBFS (with bed) = 24.5 dB quieter
  gaps (wholesale video 1 v3 verification).
- **Brand Beats / promo / interview:** continuous music bed, ducked under
  the voice (sidechain 4–6 dB; agent-video-editor methodology: music
  18–25 dB under voice, ducking 6–12 dB, attack 10–50 ms, release
  250–700 ms). Bed runs under the ENTIRE video including pauses (zero dead
  air). Melody-free beds under long talking; music with vocals fights
  speech. Edit music on its phrases; end on a real ending or a fade.
- **Story videos:** somber piano bed (CC0 family: `music-emotional-piano-loop.mp3`
  primary, `music-contemplation.mp3` fallback), continuous, ducked 5–6 dB
  under voice. Reference story bed sits ~6 dB under voice in gaps.
- Music levels (agent-video-editor): music 18–25 dB under voice; SFX
  12–24 dB under voice (default 15 dB); ambience/room tone ~30 dB under
  voice. Gains COMPUTED, not guessed:
  `gain = 10^((voice_lufs − under_voice − sound_lufs)/20)`, capped at 1.
  If it comes out above 1, pick another sound rather than amplifying.
- Room tone under every gap left by a cut (~30 dB under voice, never
  digital silence). No room tone? Copy the cleanest quiet stretch from the
  recording itself.

## SFX grammar

- SFX on beats only: card in, stat reveal, section change, CTA. No SFX on
  every single word. No long SFX tails, no risers that fight the voice.
- Place the transient 2–4 frames BEFORE the visual change so the peak lines
  up with what is seen. Trim silence at the start of the file first.
  (SFX Kit sounds carry sync points: start every sound at the moment it
  should meet MINUS its sync offset — see `11-sfx-inventory.md`.)
- Limits (agent-video-editor methodology): NO whoosh on every continuity
  cut; same sound max 3× in a row; never louder than voice or on a key word
  (a number, a name); no sounds over real recorded sounds that already do
  the job.
- Typing SFX: trimmed to grapheme-count/cps, −9 to −10 dB; sits 15.9–19.1
  dB under voice RMS per span (background texture under dense speech,
  audible in micro-pauses). Only for numbers/addresses actually spoken.
- Whooshes: DROPPED from wholesale video 1 after sample evidence showed
  them inaudible under dense speech. In story videos, soft whoosh only on
  major section changes. Stacking whoosh effects is NOT sound design (user
  verdict on Takbir design mix, 2026-11-13).
- Story videos: SFX follow the SPOKEN WORDS; numbers/graphs/bell/knock get
  extra storyline-based SFX; counters get supporting story-world sounds
  tied to the spoken word, never generic UI pops. (User rule, 2026-11-13.)
- Full inventory, timing/mix rules, and per-video usage:
  `11-sfx-inventory.md`.

## Silence, pauses, fillers

- Promo/interview: zero dead air (see `02-style-and-editing.md` §1).
- Wholesale video 2 pause rule: gaps ≥0.4 s tightened to 0.20 s, gap head
  kept — 82 cuts, 55.21 s removed. Cut decisions re-verified against
  50 ms energy profiles; 0 words inside cuts; monotonic times. Do not cut
  inside stretched words.
- Fillers: remove genuine filler non-words one by one. Wholesale video 1:
  4 ASR passes found ZERO genuine fillers — nothing removed, duration
  unchanged. A Whisper 'uh' candidate at p=0.03 inside a hallucinated
  segment was rejected. Wholesale video 2: 0 fillers found.
- Unintelligible spans are PROTECTED: no words, no cuts, audio preserved.
  (Wholesale video 2: 10 spans. Wholesale video 1: 7 spans incl. 138–157 s
  and 220–245 s.)

## Mix traps (proven)

- **amix collapses to mono** when its first input is a mono MP3 upmixed
  in-graph — pre-convert EVERY input to stereo 48 kHz WAV first.
- **sidechaincompress truncates output** when the voice sidechain ends —
  apad the voice branch to full duration.
- **loudnorm upsamples to 192 kHz** — aresample to 48000 after it.
- **Mono SFX stereo pan bug:** `pan=stereo|c0=c0|c1=c1` on a MONO file maps
  a nonexistent input channel to the right output → silent right channel
  (ch1 peak −180 dB). Always use `c1=c0` for mono sources.
- **s16 premaster clipping:** a 16-bit premaster clipped 699 samples in 201
  runs at cue+voice peak coincidences — write the premaster as float.
- **ffmpeg cue graphs hang** — wholesale video 2's mix used numpy only for
  the SFX mix (clicks −3 dB, pops 0 dB, typing −9 dB, quietest-window
  placement), then 2-pass loudnorm + makeup + limiter.
- **LSD is confounded** as a denoise quality score: removing noise itself
  raises LSD. Use only as a rough "how much did the spectrum change" signal.
- The `loudnorm` report goes to STDERR, not stdout: reading stdout gives
  nothing.
