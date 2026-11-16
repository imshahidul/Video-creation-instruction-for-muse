# 08 — Story videos

Long-form narrated story videos from Saimon Alam Shovo ("Shuvro")'s Bangla
stories (Saimstory): 'ঢেউ' (Dheu) and 'তাকবির' (Takbir). Different family
from promos: slow, cinematic, faceless 2D animation. NO watermark. NO
follow card (Takbir). The no-copied-names rule for Brand Beats mock UI does
NOT apply to intrinsic story names (Rahim Chacha, Suman Bhai, etc.).

## Style reference: "দশ ভাগের এক ভাগ" (Ashik AR)

Studied frame by frame (2 fps contact sheets + full-res keys). Study notes:
`~/workspace/story-video/ref-study/STUDY_NOTES.md`. Source: 194.05 s,
1280×720 (16:9 landscape), 30 fps, ~27 shots, avg ~7.2 s per shot, uniform
slow pacing (~8 dissolves/min). Only 3–4 hard cuts; most transitions are
0.3–0.5 s cross-dissolves (sometimes through a bright haze). Fade-to-black
only at title card and end.

- **Visual medium:** 2D FLAT VECTOR ANIMATION (custom motion design,
  After-Effects style). NOT photos, NOT AI images, NOT live footage.
  Faceless dark silhouettes with warm rim light; gradient skies; minimal
  detail; wide cinematic compositions, characters small in frame. Palette
  per scene: navy night, sepia/golden day, warm brown interiors, parchment
  (story-within-story, framed border + vignette), grey airport, purple dusk.
  Recurring motifs: moon, suitcase, glowing phone screens, gold coins,
  trees, stars, red beacon lights.
- **Camera STATIC within shots** (verified: identical framing across
  seconds). Only micro-ambient motion: twinkling stars, blinking beacons,
  slight sway. Character animation (rig): walking, arm gestures, handing
  objects, head turns. Animated props: plane, coins, counters, growing
  tree, year ticker, moving sun. THIS is the part stills cannot reproduce.
- **On-screen text: NO bottom captions anywhere.** Kinetic typography, upper
  third, top-left or top-right, left-aligned, 2–4 lines, generous leading.
  Bold Bangla sans (~40–48 px at 720p). Word-by-word/line-by-line
  accumulation synced to narration; clears between sentences. Key words pop
  in colored: GOLD (#F5B942-ish) = key facts/numbers, RED (#D94A3D-ish) =
  emotional/high-stakes/dialogue — refined: red also marks dramatic numbers
  ("বাইশ।", "৫০°"), not a clean facts/emotion split. Dialogue in speech
  bubbles: white = normal, red-tinted = emotional. Title card: tagline +
  HUGE title + motif row (10 gold coins), blur-in. Notebook scene:
  handwritten-style red Bangla + animated pen. Watermark bottom-right on ALL
  reference frames ("আশিকের গল্প · Ashik AR") — the reference's watermark,
  NOT to be copied (our story videos carry NO watermark).
- **Audio:** male baritone narration (median F0 ~100–111 Hz), slow
  deliberate pace, pauses at emotional beats. Continuous ambient/cinematic
  music bed, no strong beat; ~6 dB under voice in gaps; no prominent SFX;
  no silence except final fade-out. Master: mean RMS −16.6 dB, peak
  −0.4 dB. Target equivalent: −14 LUFS.
- **Structure:** hook (punch line first) → title card → backstory → drain →
  warning → book → lesson (+callback) → applying → time-lapse → test →
  callback + notebook → CTA → follow end card → fade-out. Title card ≈13–15 s.
  Second title beat restates the title huge in RED with the 10-coin row
  (title callback). Infographics: remittance graphic, expense cards + total
  counter (green ✓ ticks as "paid"), savings cards, DPS paper card, document
  cards, book-cover glow showcase, notebook page with animated pen + 3
  numbered rules, coin rows, year ticker + growing counter. Split-screen
  used TWICE. End card: Follow button animates Follow → Following and
  carries the video's ONLY photographic face (avatar photo).

## Build mapping (ঢেউ / তাকবির)

- Output: 1280×1024 (5:4), 30 fps, H.264 CRF 18, AAC 160k stereo 48 kHz,
  faststart. (16:9 vs 4:5 was an open question for ঢেউ; 5:4 was used for
  Takbir.)
- Visuals: 2D flat vector, faceless dark silhouettes with warm rim light,
  gradient skies, minimal, characters small in frame, lots of upper-third
  negative space. NO realistic people, NO faces, NO close-ups. Characters
  stay consistent across shots (locked descriptions per character). Prefer
  object/landscape scenes where the story allows (calculator, ventilator
  monitor line, chart times, prayer mat, tasbih, folded dua paper, dawn
  mosque).
- Characters (locked descriptions, silhouette only — Takbir): Narrator =
  young/mid adult Bangladeshi man silhouette, dark shirt, bank employee;
  Abba = elderly silhouette, white panjabi, white prayer cap, grey beard
  silhouette, headmaster; Rahim Chacha = ~60 silhouette, white beard, ward
  boy uniform, flask; Suman Bhai = nurse silhouette, ICU; Imam = silhouette,
  prayer cap. Back/side views, never faces.
- Pacing: slow ~7 s shots, 0.4 s cross-dissolves, static camera, optional
  1.00→1.03 drift on emotional beats only. Fade to black only at title + end.
- Text: upper-third kinetic Bangla ONLY, no bottom captions at all. Hind
  Siliguri Bold, PNG overlays via PIL+libraqm (never libass/subtitles
  filter). White main, gold for key facts/numbers, red for emotional/
  dialogue. Word/line accumulation synced to narration via silencedetect +
  RMS phrase timing in story order (never Whisper word timings). Speech
  bubbles: white normal, red-tinted emotional.
- Counters/cards use EXACT story numbers (Takbir: 52 waqts, 54 with Eid,
  1825, under 3%, 21,600 breaths/day, 15/min, every 4 seconds, prayer chart
  times vs azan times exactly one minute after every time, 40 years, 73,000
  times, 30 years, 8th day, Fajr 4:50/4:52, bed 7, 3 knocks motif, dua list
  paper reveal).
- Title card: huge title + tagline chosen by best judgment. Builder records
  the choice in the report.
- Music: somber piano (CC0 bed family: `music-emotional-piano-loop.mp3`
  primary, `music-contemplation.mp3` fallback), continuous bed ducked 5–6 dB
  under voice, soft whoosh only on major section changes, master
  −14 LUFS / −1 dBTP.
- NO watermark anywhere. NO follow card (Takbir). End card = credit only
  (title + author credit exactly as given: "তাকবির" / সাইমন আলম শুভ / শুভ্র /
  ১১/১১/২৬) + fade to black. Do not invent a follow/comment/share ask.
- Tasteful handling: ICU/ventilator/death/janaza scenes as silhouettes +
  objects + monitor line only. No graphic medical detail, no bodies, no
  faces. Prayer scenes respectful, silhouettes only.
- Honest gap (same as ঢেউ): no rig animation; staged stills + counters +
  dissolves only. Characters do not walk/gesture. Cannot reproduce: rig
  character animation, true time-lapse growth (approximate with staged
  stills + counters), handwritten Bangla font (fallback red Hind Siliguri +
  pen).
- Voiceover: ElevenLabs Rahat Narrator, user-supplied, used exactly at full
  length. Do not regenerate. (Takbir VO: 657.868 s, 44.1 kHz mono.)
- Verification (mandatory): ffprobe specs + faststart, loudness numbers,
  10+ frame QA spanning all sections + title + end card (conjuncts intact,
  upper-third text unclipped, no bottom captions, no watermark, no follow
  card, no faces, counters/times correct, credit exact).
- Delivery: build + verify + deliver the file to the user for verdict. Do
  NOT upload or post anywhere without a separate user instruction.
- Queue discipline: Takbir was ordered while ঢেউ was still building — start
  only after ঢেউ finished AND was verified; do not run concurrently (shared
  CPU + Pollinations rate limits).

## Illustrations

- Pollinations flux, 1280×1024, style-locked prompts (flat vector, faceless
  silhouettes, rim light, gradient sky, no text in images), 503 → wait 45 s
  + retry, crop watermark strip if present, verify every image on contact
  sheets (no faces, no text, no watermark). Silhouettes hide character
  inconsistency. Expect ~55–70 shots for 658 s at ~7 s + reuse for
  callbacks; ~45–55 unique illustrations.
- Reuse compositions for callbacks like the reference does.

## Sound design rules + the Takbir history (read before touching story audio)

- **SFX follow the SPOKEN WORDS** (user rule, 2026-11-13 08:56 — verbatim in
  `01-standing-rules.md`). Numbers/graphs/bell/knock get extra storyline-
  based SFX; counters/stat cards get supporting story-world sounds tied to
  the spoken word, never generic UI pops.
- **Cue audibility vs the voice** (see `03-audio-and-voice.md`) — proven
  twice on Takbir (v1 soft SFX, v5 cues 19–21 dB under voice peaks).
- **Takbir: FOUR rejected audio passes, then DROPPED.** v1 soft SFX; v2 loud
  accents; v3 design mix (399 events: 72 transition whooshes + 297 ticks +
  30 beat accents) — user: "শুধু তো হুইশ ইফেক্ট বসালেই সাউন্ড ডিজাইন হয়ে
  যায়না"; v4 repo mix (agent-video-editor methodology) — user: "মন মতো
  হইতেছেনা। সাউন্ড ডিজাইন আরো শিখতে হবে তোমার". No version approved; do not
  upload any of them. **USER DROPPED IT 2026-11-13 11:09**: "আচ্ছা বাদ দাও।
  এইটা অনেক বড় হওয়ায় হয়তো ঠিকঠাক পারতেছো না। গ্রাফ, টেক্সট স্ক্রিনে আসার
  সাউন্ড এগুলো নাই।" **Do NOT resume Takbir sound work without explicit
  user instruction.** All 5 mixes + plan stems/scripts kept in
  `~/workspace/takbir-video/build/plan/`.
- The agent-video-editor sound-design methodology (kmilo93sd/
  agent-video-editor, cloned at
  `~/workspace/brand-beats-videos/audio/agent-video-editor`) was the v4
  basis: voice alone −16 LUFS; room tone under every gap (~30 dB under
  voice, never digital silence); music 18–25 dB under voice with ducking
  6–12 dB; SFX gains COMPUTED; SFX sparingly and only confirming on-screen
  action — explicitly NO whoosh on every continuity cut, same sound max 3×
  in a row, never louder than voice or on a key word, transient 2–4 frames
  before the visual change. Master −14 LUFS / −1 dBTP two-pass loudnorm.
  It did NOT close the user's complaint — the methodology is recorded, not
  endorsed as sufficient.

## New story refs — decisions OPEN (2026-11-16, do not assume)

Four decisions pending from the user for the new story-reference builds:
(1) voice — Melody vs TruthTeller; (2) bars — black like the refs vs cream
(standing no-black-background rule); (3) pace — ref-faithful ~1 s cuts
(70–100 pictures/video) vs 16–18 pictures held 5–7 s each; (4) which story
first (murgi or fisherman) + end-card branding for the heyyimshahidul
profile (Follow card or none). No full video built, nothing posted/uploaded
as of the 2026-11-16 12:40 presentation.
