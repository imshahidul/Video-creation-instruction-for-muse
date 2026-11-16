# 02 — Style and editing

Source of truth: `~/workspace/interview-edit/study/STYLE_GUIDE.md`, distilled
from frame-by-frame study of 13 reference YouTube Shorts (2026-11-13) and
re-verified at 10 fps against 28 reference videos (2026-11-14). Where this
file and an older study note disagree, the style guide wins for editing
style; the standing pipeline rules (Hind Siliguri + PIL/libraqm captions,
never libass; no copied names in mock UI) still stand. This file is a
condensed faithful copy — the full guide, with all timings and the 20-item
corrections log, lives at that local path.

## 0. The two families (pick one per video, never mix randomly)

- **Family A — Kinetic type, no speaker.** No speaker on camera. The screen
  is a motion-graphics canvas: floating cards + huge typography carry the
  whole video. Faces may still appear inside B-roll photos/posters — "no
  face" means no speaker, not no face anywhere. Use for explainers, tool
  roundups, list videos, and any video where no good talking-head footage
  exists.
- **Family B — Talking head + B-roll.** Speaker on camera + B-roll
  cards/screens that swap constantly. Use for interviews, podcast clips,
  demos, and founder videos. This is the family for the KM Enterprise
  interview edit.

## 1. Format (measured)

- Aspect 9:16 vertical, 25 or 30 fps, for all promo/interview/IG material
  (story ref is the 16:9 landscape exception; IG3 is 24 fps, ref2 is
  60 fps). Source footage may be 3:4 or 4:5; keep the source aspect for
  interview edits, do not crop the speaker to 9:16. Wholesale/sales videos
  are 4:5 (1080×1350) per user rule — see `01-standing-rules.md`.
- Duration: 18–87 s across the 13 Shorts; sweet spot 30–65 s. Full 28-video
  set runs 10–194 s.
- Loudness: master to **-14 LUFS integrated, -1 dBTP**. This is a BUILD
  STANDARD, not a measured reference trait: 8/13 Group A true peaks exceed
  0 dBTP (up to +0.95), and R2's master clips at +4.2 dBFS — do not copy
  either. Reference masters span -8 to -21 LUFS (median ≈ -14).
- **Zero dead air.** Measured: 0 silence gaps ≥ 0.4 s at -45 dB in the
  sampled Shorts. A music bed and/or room tone runs under the ENTIRE video,
  including pauses. Never leave digital silence — except a DESIGNED silence
  beat where the story earns one (only two verified examples in 28 videos).

## 2. Cut / B-roll rhythm (measured)

- A new visual every **1.5–4 seconds**. Never hold a FROZEN shot longer
  than ~5 s. Family A holds reach ~5 s only while in-place animation
  continues. Talking-head family averages one B-roll swap every 2–4 s.
- B-roll is **script-matched**: the picture shows what the voice is saying
  AT THAT SECOND (tool named → tool UI; number spoken → stat card; place
  named → that place). Random pretty B-roll is not this style.
- B-roll layouts (all three are used; pick per beat):
  1. **Full-frame B-roll** — screen recording / photo / clip fills the
     frame, captions over it.
  2. **Split card** — B-roll card on the top ~55%, speaker in a rounded
     frame on the bottom ~45%.
  3. **Floating card** — B-roll as a tilted/rounded card with soft shadow
     on a plain background (kinetic family).
- Phone content: show it as a **phone mockup or full-screen phone
  recording**. Never a PC browser window for mobile content.
- Stat cards: when a number is spoken, a card with the BIG number + short
  label appears. Numbers get their own beat; never bury a number in small
  caption text only. Count-ups are a verified variant (number counts up on
  the card).
- Numbered sections: "Plugin Number One", "#1/5 … #5/5" cards mark list
  items. Use for any list of 3+ items.
- Verified effects vocabulary (10 fps): glitch-in stat entrances, icon
  stagger-pops + icon morph/swap, annotation arrows + circle highlights,
  film-frame/HUD borders + timecode, sub-second image cycling, type-on with
  cursor, graphic prop overlays, badge/slider rails, arrow-mapping +
  node-link diagrams, persistent card frame with in-card swaps +
  interstitial title cards, simultaneous stacked role videos, split-screen
  meme+speaker hook.
- Zooms/punches: subtle scale punches on emphasis beats. No slow Ken Burns
  drift as the only motion; motion must feel cut-driven, not
  slideshow-driven. (Ken Burns acceptable ONLY for still B-roll images,
  paired with a cut every 2–4 s.)

## 3. Captions (the single most consistent rule)

- **Text synced to speech is the rule; word-by-word captions are the most
  common system, not the only one.** Verified taxonomy: 7 standard
  word/phrase caption systems, 3 kinetic-type-as-caption (words build
  gray→black, no separate caption layer), 1 fragmentary/labels-only, 1
  tiny-chip system, 1 with NO captions. Pick ONE text system per video and
  keep it consistent.
- Position depends on layout: bottom-center (talking head, full-frame),
  CENTER between card and speaker frame (split layouts), MID-FRAME at ~55%
  height, RIDING graphic elements, UPPER third (story animation). Never
  covering the speaker's face.
- Style: bold sans, white with black outline/shadow on dark footage; black
  on light backgrounds. 1–4 words visible at a time, building a phrase,
  then clearing. Short phrases, not full sentences.
- **Keyword emphasis is mandatory.** Important words get a SECOND style:
  italic serif, yellow, blue, orange-red, or a HIGHLIGHT BOX. Grey→white
  upcoming-word mechanic: upcoming words grey, spoken words turn
  white/black. Pick ONE accent per video and use it only for keywords.
- Kinetic family variant: words pop in one by one with mixed sizes — huge
  bold black for the key word, small gray for lead-in words, upcoming words
  gray → spoken words black. Lists build line by line.
- Bangla captions: Hind Siliguri Bold, rendered as PNGs via PIL + libraqm
  (Layout.RAQM), overlaid as a video stream. NEVER the ffmpeg
  subtitles/libass filter — it breaks Bengali shaping. Verify conjuncts on
  final frames.
- Captions must match the SPOKEN words exactly and sit on the spoken
  second. Never paraphrase in captions.

## 4. Sound design

- **Continuous music bed**, ducked under the voice (sidechain, 4–6 dB), for
  the whole duration — EXCEPT wholesale/sales videos, where the user rule
  is NO background music (voice + SFX only). Bed genre: upbeat
  electronic/lo-fi for tool videos; keep it low and steady — the voice
  leads.
- **SFX on every visual beat**: soft pop/click when a card or caption word
  lands, whoosh on full-frame swaps, stamp/thud on stat cards. Honest
  limit: individual SFX could NOT be isolated from the reference waveforms
  (speech dominates); this rule is the genre grammar, not a measured SFX
  list.
- **Cue audibility rule (hard):** every cue's peak must clear the VOICE at
  the same second, or sit in a real speech gap. A margin measured against
  the music proves nothing. Measure per cue, per second.
- No long SFX tails, no risers that fight the voice, no SFX on every single
  word (only on beats: card in, stat reveal, section change, CTA).
- Voice processing: light compression + high-pass ~80 Hz; voice sits 10+ dB
  over the ducked bed at all times.

## 5. Transitions

- **Hard cuts** are the default in cut-driven videos (dominant in 11/13
  Shorts). Jump cuts on the speaker are fine and expected.
- Kinetic family: animated moves instead of cuts — cards fly/scale/slide
  in, text pops, lists build. Zero-cut videos exist: motion carries the
  whole video.
- **Verified non-cut transitions** (10 fps): blur frames, white flash,
  cut/fade-to-black hold, slide/wipe, motion-blur entrances, glitch,
  vertical motion-blur smear, star wipe, red flash, invert flashes, 90°
  frame rotation + background shatter.
- **No TRUE cross-dissolves** between beats in promo/interview/IG videos
  (zero found in 25 videos). Exceptions belong to DIFFERENT families:
  dissolves are the NATIVE grammar of long-form story animation (0.2–0.6 s),
  and blur-dissolves are acceptable for same-subject shot changes in calm
  talking-head footage. A short fade in at 0 s and fade out at the end is
  always fine.
- Card entrances: quick scale-up (0.95→1.0) + fade, honest range ≤0.1–0.3 s
  by element (~0.15–0.25 s typical), with a soft pop. Keep entrances
  uniform within one video.

## 6. Framing and look

- Speaker: medium close-up, centered, eyes in the upper third, mic visible
  is fine. Plain or softly blurred background; no clutter behind the head.
- Color: ONE background world per video is the NORM — clean light
  (off-white #F2F2F2, soft peach/lavender gradients) OR dark — plus ONE
  accent color. Documented exceptions alternate worlds only at section
  changes, with a reason. Never two competing accents without a system.
  (Standing user rule overrides: NO black/dark backgrounds — light
  background + beautiful decorative frame. See `01-standing-rules.md`.)
- Cards: rounded corners, soft drop shadow, thin border optional. Screens
  and UIs always appear as CARDS with margins, never edge-to-edge
  screenshots (except full-frame phone recordings).
- Title/hook cards: huge condensed bold headline in the first 1–2 s stating
  the payoff. The hook is a promise, not a greeting.
- End: choose ONE of three verified patterns — (1) CTA card ("Comment
  KEYWORD" + follow prompt), (2) follow / pin-comment / logo end, (3) COLD
  END on the payoff frame. A fourth: a PERSISTENT CTA footer pinned for the
  whole video. No logo sting longer than 1 s.

## 7. Structure

1. **Hook (0–3 s):** big headline + the payoff. No intro, no greeting.
2. **Body:** one point per beat, B-roll matched to the words, stat cards on
   numbers, numbered cards on list items.
3. **Payoff/CTA (last 3–5 s):** the result + the chosen ending. No outro
   music tail (except a designed quiet tail).

## 8. What to avoid

- Frozen shots held past ~5 s with no in-place animation; slideshow pacing.
- Full-sentence static captions; captions that lag the voice.
- True cross-dissolves between beats in promo/interview/IG videos; slow
  fades mid-video.
- Unsystematic multi-accent color / rainbow text.
- Dead air / gaps with no bed.
- B-roll unrelated to the spoken words at that second.
- PC browser screenshots for mobile content.
- Generic praise captions — every word on screen must be a spoken word or
  a stat/label.
- Watermarks from other creators' tools, and copied names/details from any
  reference (mock UI must use invented names, never the reference's).

## 9. Build checklist (per video)

- [ ] Family chosen (A kinetic / B talking head) and kept consistent.
- [ ] Word timings measured from the real audio (never a global chars/sec rate).
- [ ] Every 1.5–4 s has a visual change; no frozen shot over ~5 s (holds
      to ~5 s only with continuous in-place animation).
- [ ] Every spoken number has a stat card beat (or a count-up on the card).
- [ ] Text system chosen deliberately; keyword accent consistent; conjuncts
      verified.
- [ ] Bed continuous, ducked; SFX on beats, measured against the voice.
- [ ] Master -14 LUFS / -1 dBTP (build standard); no clipping; faststart on.
- [ ] Hook in first 2 s; ending chosen deliberately.
- [ ] Frame QA: 10+ frames read visually, captions + B-roll match the words.

## 10. Motion grammar (FB reels, measured timings)

- Card entrance: rise from bottom, slide from the side, or fade/scale in
  place — honest range ≤0.1–0.3 s by element. Stamps/badges: INSTANT pop
  (≤0.1 s) or a small tilted fly-in that never levels — NEVER a rotation
  slam.
- Full-scene change: zoom-blur out → flash, core ~0.4 s, new elements
  staggering in to ~1.5 s total. Second grammar (same background):
  zoom-out-to-blank + type/fade-in, no blur/flash.
- In-card content swap: dip ≈0.2 s + WHITE flash frame + blank hold ≈0.5 s
  + progressive build ≈0.6 s, title changing before body; frame fixed.
- B-roll swap under a continuous speaker: HARD CUT every 0.4–0.7 s; the
  speaker never cuts, only the card swaps.
- Data animation: slow eased sweeps — gauge needle ~1.3 s in-window with
  arc fill; checklist traveling glowing dot ~0.9–1.0 s per row, checkmark
  pop per step.
- Text build: word-by-word fade + rise, ~0.3 s per word; keyword highlight
  applied AS THE WORD IS SPOKEN; lines draw on left-to-right.
- Never-static: every held element has idle motion (bob/pulse/drift/glow)
  or the frame changes within ~4 s. Photos must move continuously.
- Beat rhythm: fast lists ~1.4 s, normal ~2.7 s, calm data ~4 s.
- Mystery-card word reveal: all "?" card frames land within 0.3 s TOTAL;
  then each card's content swaps to the spoken word one at a time, reveals
  staggered ~0.2–0.3 s apart, synced to speech.
- Toggle / state flip: fast (≤0.1 s) UI state change synced to the spoken
  keyword. Strike-through device verified; a green ✓ post-flip badge was
  NOT verified — do not cite an ✗→✓ badge swap.
- Exits — THREE grammars: instant pop-out (≤0.1 s), fast group fade
  (~0.1–0.2 s), or hold.
- Semantic caption colors (OPTIONAL variant): keyword color follows meaning
  — green = positive/sales, red = negative, cyan = English terms, yellow =
  emphasis, purple = people/message — used consistently across the video.

## 11. IG reels appendix (10 fps)

- **Zero-cut morph continuity:** full-video shared-element morph chain
  (dot → cursor → prompt pill → app card → chart → wordmark → terminal →
  timeline → slides → bar → dot), zero hard cuts, closed loop so the video
  loops seamlessly. Plan the loop before building: first and last frames
  must be the same element. HUD proof counter ("CUTS 0" / "TAKE 01") turns
  the technique into content.
- **Before/After showcase:** small flat "Before" card + large graded "After"
  card; the Before card plays untouched while EVERY edit happens inside the
  After card only. Grade flip (color↔B&W) as a section device.
- **Curved-path captions + 3D type:** words follow curved paths around the
  speaker; 3D extruded keyword type, one per beat max; invert flash (1–2
  frames); 90° frame rotation transition; background shatter; drawn string
  through floating photos; shaped-frame background swaps.
- **Gradient type, pills, streaks:** gradient keyword typography; floating
  pill labels tracking a moving subject; light-streak motif; photo halo;
  call-UI overlay as a B-roll device; blur-dissolve exception for
  same-subject shot changes (three verified).
- **Count-graphics warning:** on-screen text disagreed with the voiceover in
  two studied reels ("49 HOMES" shown while VO says 50). Check every
  on-screen number/word against the VO; never assume they match.

## 12. SFX-demo Shorts appendix

- **Scrolling-timeline demo format:** fixed playhead + timeline of waveform
  clips scrolling at CONSTANT speed + label naming the clip under the
  playhead + pinned header/footer. Zero cuts. Clip width = sound length —
  the timeline honestly maps time to space. Label swaps ~0.2 s fades.
- **Countdown + pulsing icon format:** 10→01 countdown, label + number swap
  on HARD CUTS, one item per ~1.3 s. Pulsing icon is DECORATIVE (fixed
  loop), not audio-reactive — do not fake reactivity.
- **SFX-demo sound grammar:** sounds play at NATIVE levels, not normalized
  (12 dB span measured). Two demo styles: ISOLATION (silence gaps between
  sounds) vs CHAINING (sounds butt against each other). Masters ≈ -14 LUFS
  but LRA 6–11 LU — dynamic, unlike speech reels. Silence is legitimate
  here; the zero-dead-air rule covers speech videos.
- **Sound-honesty scope:** the "no individual SFX verifiable" rule was
  proven on SPEECH-DENSE mixes only. In SFX demos, a label + measured burst
  proves a distinct sound event with a stated envelope; it never proves the
  sound "sounds like" its label. Take sound names from labels, never from
  spectra.

## 13. Signature-edit, ref2, and story-ref systems

- **Signature edit:** frozen outer frame all 23.9 s; small tilted SOURCE
  card playing RAW footage continuously; large SIGNATURE card where ALL
  editing happens; persistent bottom CTA footer. Mixed-style kinetic type
  clusters inside the card (the MIX is the style); words rotate freely;
  white + red only; no bottom captions. Outer frame ZERO cuts/transitions.
- **Brand Beats ref2 (10.24 s, 60 fps):** one continuous take + PER-SECTION
  DIGITAL REFRAMING (zoom punches per section, not a locked-off camera).
  Huge bold condensed/italic red-gradient display caps; text-behind-head
  layering; thick dark-red-border tilted overlapping REAL photo cards;
  glitch / motion-blur smear / star-wipe transitions; zero hard cuts; ends
  cold. (User override stands: Brand Beats versions without people.)
- **Story ref ("দশ ভাগের এক ভাগ", 194 s, 16:9):** 2D flat vector animation,
  faceless silhouettes, static camera within shots, micro-ambient motion,
  ~27 shots, 4 hard cuts, DISSOLVES 0.2–0.6 s as native grammar. NO bottom
  captions; upper-area kinetic Bangla text; gold = key facts/names/amounts,
  red = dialogue + emotional/high-stakes emphasis INCLUDING dramatic
  numbers. Infographics: counters, expense cards, coin rows, year ticker.
  End card: Follow button animates Follow → Following. See
  `08-story-videos.md`.

## 14. FB1D long-form tutorial — adopted teachings (2026-11-14)

Reference: 10:34 landscape Bangla tutorial by Md Ashik Ali teaching his
motion-graphics pipeline with Claude. User order 2026-11-14 07:34: apply
what the video says. Evidence:
`~/workspace/interview-edit/study/refs2/FB_SHARE_1DKM7SctjD_NOTES.md`.

ADOPTED into standing practice:

1. **5-point preview QA checklist** — before any final render: (1) every
   text arrives on exactly the right word; (2) no text/picture goes
   off-screen; (3) subtitles readable; (4) sound/music does not bury the
   voice; (5) no scene feels empty or monotonous. Fix ONLY the flagged
   scenes, never rebuild the whole video.
2. **Dual-script equal-word-count trick** — for mixed Bangla+English
   scripts: voice file with English words written in Bangla letters (so
   TTS pronounces them right), subtitle file with English words in
   English, EQUAL word count per line, so VO and on-screen words match
   word-for-word.
3. **Voice-script number/word rules** — numbers always in words in voice
   scripts, never digits; words the TTS cannot pronounce are excluded
   from the script.
4. **Voice-first + scene-plan approval** — voice before video always;
   word timings to fractions of a second; scene plan shown/approved
   before building.
5. **Chunked render + join** — for long videos, render in chunks and join
   (disk + resume benefits); single render remains fine for shorts.
6. **Screenshot-rebuild rule** — never paste a raw screenshot into a
   video; rebuild the app UI from it (sharper + no personal info).
   Extends the privacy rule (never show real DOB/Gmail/card).
7. **Subtitle pill + current-word accent** — a new caption system option
   for LONG-FORM: small white pill, current spoken word in the accent
   colour. Shorts keep the existing karaoke/kinetic systems.
8. **Count-up numbers from zero** — Bengali digits + growing bar variant.
9. **Motion vocabulary** — camera push-in on app UIs; cursor click with
   ripple; type-on letters. Village-example device (rickshaw/boat/kitchen)
   available for explaining hard ideas.
10. **Skill-improvement loop** — after every video, fold what was learned
    back into the guide / AGENTS.md. (This repo is now part of that loop.)
11. **Script rules** — research first; Bangla+English as actually spoken;
    simple enough for a class-7 child; "halve that sound" as the fix
    instruction for a loud cue.
12. **Long-form structure option** — hook → reveal → process overview →
    icon-titled sections → recap diagram → encouragement →
    keyword-comment CTA + follow end card, for long-form only.

Deliberately NOT adopted (conflict with a standing user rule):

- **Graphics-only world** — the reference uses ZERO real footage/photos.
  The user's FOOTAGE RULE wins. Transferable lessons are the systems, not
  the world.
- **Dissolves in shorts** — scoped to long-form. The shorts hard-cut
  default stands.
- **Whoosh vocabulary in story videos** — does not override the
  story-video SFX rules.
- **Brand package + names** — the purple/paper/dots brand as a package,
  "Md Ashik Ali", "ashik-motion", and the Motion Skill Guide book are
  do-not-copy (no-copied-names rule). Tool names it teaches (Claude,
  Remotion, HeyGen HyperFrames, Anthropic, Cartesia, GitHub) are subject
  matter, fine to reference as tools.
- **Voice -16 / music -30 LUFS stem claim** — an on-screen claim, not
  measured. The standing master standard (-14 LUFS / -1 dBTP) is
  unchanged.

## Honesty limits (stand unchanged)

- No individual SFX is verifiable in any of the 25 speech mixes
  (re-confirmed in the 10 fps pass). Bed presence beyond silence-gap
  inference, ducking amounts, bed genre, and voice-over-bed margins were
  NOT measured. Caption word-accuracy vs speech was NOT checked in the
  study pass. Exact easing curves and exact hex colors (story ref, ref2)
  were NOT measured. SFX placement follows user direction + the
  voice-relative cue rule, never a waveform claim about the references.
