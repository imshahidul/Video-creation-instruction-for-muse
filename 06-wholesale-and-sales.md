# 06 — Wholesale and sales videos

Two related families. **Wholesale videos** (KM Enterprise, speaker Rakib):
full-caption karaoke style, built November 2026. **Sales videos** (Right
Choice showroom garments + Dulha Panjabi): key-points-only overlays,
Gemini-photo B-roll, hook-first. The standing rules in
`01-standing-rules.md` govern both; this file holds the build systems,
verified specs, and per-video facts.

## Identity facts (do not mix up)

- **KM Enterprise** — wholesale shop, speaker **Rakib**. Videos: denim
  jackets (video 1) and jeans (video 2). Shop C-62, Mirpur 1, Shah Ali
  Market / College Market. WhatsApp 01834 963 786 (spoken once in video 1,
  ~196–202 s; grouping on cards normalized to the video-1 verified form —
  see flags below).
- **Right Choice** ("রাইট চয়েজ") — showroom garments. Sales videos 1–2
  (vests, blazers). Name verified from visible evidence (bag + garment
  tags in footage).
- **Dulha Panjabi** ("দুলহা পাঞ্জাবি") — DIFFERENT shop. Sales video 3
  (panjabis) ONLY. Never mix names/addresses/phones between Right Choice
  and Dulha Panjabi.
- NOT Dulha Panjabi for KM/photos: an early wrong assumption; the file
  `~/workspace/your_files/dulha-panjabi-voiceover.mp3` was never used.
- The user edits videos himself afterward; Muse builds, he finishes.

## Wholesale video 1 — KM Enterprise denim jackets (COMPLETE, closed)

- Source: `~/workspace/wholesale-video/source/MVI_2196.MP4` (971,687,504
  bytes, 261.6 s, 1920×1080 25 fps; Drive ID
  `1iHRSz9f-l1eC3anpWSxUidlryLRFRX2v`). Single static camera, one shop,
  consistent tube lighting, no scene changes.
- **Delivered v3** (verified): `km-enterprise-wholesale-full-v3.mp4`, md5
  `e0110700b28116779f756d1c9ad8122e`, 247,884,833 bytes, 1080×1350, 30 fps,
  261.75 s, −14.59 LUFS / −1.56 dBTP, no music, transcript = user's edited
  file verbatim (389 words). Also on the user's Drive. v2 SUPERSEDED —
  never deliver. v1 sample `dulha-sample-20s-v1.mp4` — never deliver.
  **v4/DFN rebuild CANCELLED by user 12:54** — do not rebuild unless asked.
- Transcript authority (READ-ONLY): `transcript-v1-phrases.txt` (backup
  `transcript-user-corrected-2026-11-15.txt`, chmod 444). Key corrections:
  shop **C-62**; শাহ আলী (chat correction; file still says শালী — the chat
  fix governs P50 + outlet card); P26 = **সুইং** গ্যারান্টি (NOT ওয়াশ);
  P19 unchanged. Two uncaptioned unintelligible spans (138–157 s, 220–245 s).
- Build note: `~/workspace/wholesale-video/FULL_BUILD_NOTE.md`.
- System: 56 phrases P0–P55; 11 callouts + 6 type-on cards; 62 zoom keys;
  27 highlight phrases; 23 gold keywords; 38 SFX cues (27 clicks + 11 pops),
  0 buried; 6 typing spans. First 20 s = approved sample exactly (asserted).
  Zero fillers found (4 ASR passes) — no cuts, duration unchanged.
- Audio v3: L-channel only (R is 7 dB quieter), `highpass=f=100, anlmdn`
  chain (the chain the user later called "very bad" — but v3 itself was
  delivered and accepted; the DFN rebuild was cancelled, so v3 stands as
  delivered). NO bed. Float premaster; loudnorm dynamic/TP−2.
- Uncertain tokens kept as heard and flagged (wholesale-era rule): "মাসে",
  "কেএম", "ফলো করেন", "ওয়াজ"→ওয়াশ (corrected in v3 per user file),
  "শরীর গ্যারান্টি"→সুইং (v3), "6 পিস এর পৃষ্ঠার", "এস কালার"→অ্যাশ (v3),
  "এভেলেবেল", "ফেব্রিক স্টপ", "14", "শালী"→শাহ আলী (v3),
  "কে এন্টারপ্রাইজ"/"কে এভেলেবেল".
- P31 judgment call (flagged): P31 stays captions-only per the v1 design
  (the cut-off 2nd address repetition gets captions only); the user's C-62
  completion would otherwise spawn a 3rd shop card. `TYPEON_SKIP = {31}` —
  one-line change + seg2 re-render if the user wants the 3rd card.

## Wholesale video 2 — KM Enterprise jeans (DELIVERED 2026-11-15)

- Source: `~/workspace/wholesale-video-2/source/1115-1.mp4` (566,975,542
  bytes, 1920×1080 30 fps, 446.8 s; Drive ID
  `1FF9lTQulLu6Bo5svEXjpZNzOF1382iCx`). **L channel is the good mic.** The
  user had pre-denoised it himself, then at sample approval (13:53) ordered
  a light background-noise clean, everything else stays.
- **Delivered file**: `wholesale-video-2-full-v1.mp4`, md5
  `537e463e5313dd688af8e69fd69c70a1`, 423,190,491 bytes, 1080×1350, 30 fps,
  391.9 s, AAC 48 kHz 192k, faststart, **−14.31 LUFS / −1.97 dBTP**.
  Drive ID `1AITOQvOGq0pmgYiWvQ8c5lKNwPC5THZR` — currently anyone-with-link
  for the publish flow; revert to private once the user confirms he
  published it himself (still unconfirmed).
- Build: DFN DEFAULT on L-channel voice FIRST (subtle on this pre-denoised
  source); 82 pause cuts (55.21 s removed); 941 words / 149 phrases; 29
  cards (24 callouts + 5 type-ons incl. address + 2 phone cards); 11 detail
  inserts; 89 SFX cues, 0 buried; 0 fillers; 10 unintelligible spans
  protected. Build note: `~/workspace/wholesale-video-2/FULL_BUILD_NOTE.md`;
  transcript: `work/full/transcript_full.txt`.
- **Flags delivered to user, decisions still his:** (1) phone cards
  "01834 963 786" vs spoken grouping "01834 96 3786" (digits identical);
  (2) address cards spell **শাহ আলি** vs video-1 correction **শাহ আলী**;
  (3) DFN effect subtle, his ear is final; (4) dark caption scrims/cards vs
  no-black-background rule (approved in sample at 13:53, two minutes before
  the rule) — restyle decision open; (5) uncertain tokens kept as heard
  (see build note for the full list).
- Approximate-timing regions: P71–P74, P90–P97, P131–P133, P138–P148.

## Sales videos — shared system (2026-11-16)

Original instruction set: DFN denoise FIRST (denoise-only-source rule), cut
silent parts, color grade, "Super HD" pro-camera look (GitHub research
allowed; be honest — no invented resolution), wholesale style, hook-first
(product-detail lines moved to front, 3–7 s clarity), Gemini photos as
B-roll, sample-first gate. User at 02:11: complete all three overnight, he
reviews in the morning.

- **VIDEO 1 (Right Choice, vests):** MVI_2209.MP4, Drive
  `10iRy2VxAjkSQNvp-qrgPHVdbWz3s-7fi`, 588,699,024 bytes, 1920×1080 25 fps,
  158.08 s. 10 vest B-roll photos. Sample complete (36.43 s, −15.42 LUFS /
  −1.68 dBTP); full v1 delivered 08:22 then SUPERSEDED by the v2 rebuild
  (too dark, spellings wrong, grade looked undone). v2 blocked mid-render
  2026-11-16 (see `04-technical-pipeline.md` environment notes); resume doc:
  `~/workspace/sales-video-1/work/BLOCKED_CHROME_2026-11-16.md`.
- **VIDEO 2 (Right Choice, blazers):** MVI_2206.MP4, Drive
  `1sOY4bGClSPbFLhYhDei1dyHKxUxfndPC`, 422,136,040 bytes, 112.96 s. 9 blazer
  B-roll photos. **Full v1 DELIVERED 11:22, 2026-11-16**: 106,757,082
  bytes, 85.30 s, −15.48 LUFS / −1.27 dBTP, Drive file
  `1BPqHpEZpJbMVOpBKmNaoU2I1-7McpoJ1` (this is the link the user has).
  Hook = worn-blazer demo → "তিনটা কালার" headline → greeting 3rd; 27.66 s
  silence cut; 13 key-point overlays in strict transcript wording; G4 grade;
  texture zooms; 10 SFX kept / 0 buried (6 dropped). Duplicate upload
  `1f86SdJzqISjaaISCiqT7bICg1NrzfING` owed cleanup (trash it).
- **VIDEO 3 (Dulha Panjabi, panjabis):** MVI_2239.MP4, Drive
  `1IhHOtx1YNhrf7LlUhr-VPy7OuISIzIb1`, 1,141,104,248 bytes, 306.56 s.
  5 panjabi B-roll photos. Transcript verified (657 words, 75 phrases;
  "দুলহা পাঞ্জাবি" one occurrence; no prices/phone; address unverified → no
  card). Blocked at render 4/10; resume doc:
  `~/workspace/sales-video-3/work/BLOCKED_CHROME_2026-11-16.md`.
- **Never mix the three B-roll sets.** Drive folder for finals: "Sales
  Videos - 2026-11-16" (ID `1Xsq8mlgoU_eOeEtAv3VsfGOiGNCE8M-l`).
- **Hook construction:** move product-detail lines to the front (audio +
  video together); greeting demoted to 3rd. Video 1 sample hook: src
  7.88–14.12 (collection/season) + src 24.24–28.14 (quality/guarantee).
  Clarity in 3–7 s.
- **Sample defects fixed in full builds (video 1):** D1 dead air 0.22–0.98 s
  at hook head (trim to ~src 8.85 + retime); D2 dead air 28.53–29.41 s
  (trim to ~src 45.95 + retime); D3 shoulder clips left edge ~26.3–28.5 s;
  D4 highlight leads speech 0.3–0.7 s at 8 phrase starts (retime to audible
  onsets).
- **Transcript discipline (sales):** `transcript_full.txt` /
  `transcript_words.json` stay VERBATIM as-heard (evidence). Corrections
  (spelling-prediction + visible-evidence) apply ONLY in caption/key-point
  data, with a FULL before→after CORRECTION LIST in the final report and a
  documented per-occurrence list (timestamps + audio verification) for shop
  names. Address spelling unverified → captions as heard, NO address card.
  Never reproduce phone numbers from box print (privacy; crop excludes it).
- **Silence analysis:** 30 spans ≥0.5 s analyzed per video; QA resolves
  whether each is effectively silent (Whisper starts can run ~0.83 s early).
  Cut decisions (≥0.8 s REMOVE, else KEEP) re-verified against word timings;
  do not cut inside stretched words.
- **No prices, no phone spoken** in sales videos 1 and 3 (verified by token
  scan for video 3). Address spoken in video 1 ~141–151 s, phonetic/
  unverified — no address card. 12 uncertain tokens flagged `[?]` in video
  1's transcript, none inside sample ranges.
- **Grades:** E2 (video 1), G4 (video 2 + prescribed for video 3), V2
  (video 3, FAILED re-validation — do not ship). See
  `04-technical-pipeline.md`. GitHub grading research (20 repos, 10
  render-tested): NO adoption. Reports:
  `~/workspace/sales-video-chain/grade-research/REPORT.md`,
  `~/workspace/sales-video-1/work/grade_v2/GITHUB_GRADING_RESEARCH.md`.
- **Enhancement:** frame-tested ffmpeg chain (hqdn3d → crop → lanczos →
  cas=0.6 → eq). AI upscalers honestly ruled out (no GPU; Real-ESRGAN CPU
  16+ hrs + flicker risk). Research:
  `~/workspace/sales-video-1/work/enhance/ENHANCEMENT_RESEARCH.md`.
- **Style:** cream/lime cards + decorative frame, key-point overlays (no
  karaoke captions), texture-zoom B-roll, 9–22 SFX (none buried), no music,
  no watermark, no invented content.

## Transcripts for user edit (2026-11-16 08:32)

The user asked for all three transcripts to edit himself ("আমায় সবগুলো
ট্রান্সক্রিপ্ট দাও এডিট করে দেই। অনেক ভুল"). Clean timestamped versions
delivered for videos 1–2 (`transcript-for-edit.txt`, 37 + 40 lines). Video
3's clean for-edit copy was never sent. **The user never sent edits back**;
his 09:22 "শেষ করো" superseded the wait (hold lifted). Right Choice address
spelling confirmation is still owed before any address card is built.
