# 01 — Standing rules

Every user-stated rule about video creation, attributed with date and the
user's own wording where known. Newest rule wins on conflict; superseded
rules are marked, not deleted.

## Wholesale / sales videos

- **Format — 4:5 (1080×1350).** (User, 2026-11-15.) Colour-grade so the video
  looks beautiful and the product pops; the subject is always in focus and
  centred; zoom in/out on product features.
- **Sound design and edit must be beautiful.** Quality stakes only — this
  does NOT mean Brand Beats branding in the videos. (User, 2026-11-15.)
- **NO BACKGROUND MUSIC in wholesale videos — voice + SFX only.**
  (User, 2026-11-15.) Applies to sales videos too.
- **Captions / key points are highlighted as spoken.** Typing SFX + display
  only for numbers/addresses ACTUALLY spoken. **Never invent a phone number,
  price, or address.** (User, 2026-11-15.)
- **Remove pauses** and filler non-words ("আহ", "আম্মম্ম") one by one.
  (User, 2026-11-15.)
- **Frame-by-frame QA before delivery.** Dense frame extraction across the
  full duration, fix + re-verify loop. (User, 2026-11-15.)
- **No stock video unless absolutely necessary; stock photos only in
  beautiful cards if needed.** Wholesale videos 1–2 used zero stock.
  (User, 2026-11-15.)
- **Sample-first gate.** Build a sample, get user approval, then build the
  full video. (Standing practice, 2026-11-15.)
- **Every video version under a NEW distinct filename.** Same-path re-sends
  serve the user cached old copies. The user now explicitly asks for a new
  file each time: "আর নতুন ফাইল দিবা". (Proven 2026-11-14; see
  `05-lessons-and-failures.md`.)
- **No Brand Beats branding in wholesale videos.** (User, 2026-11-15.)
- **Never silently fix uncertain caption tokens — keep as heard, flag them.**
  (Wholesale era, 2026-11-15.) SUPERSEDED for sales videos by the
  spelling-prediction rule below (2026-11-16 08:29). The wholesale builds
  kept tokens as heard; the sales builds predict proper spellings.
- **The user's edited transcript file is authoritative verbatim.** Numbers,
  addresses, and shop details must stay exactly as spoken, never invented.
  (Standing.)
- **Denoise: ffmpeg chains REJECTED as very bad** (user, 2026-11-15 12:26).
  **DeepFilterNet (DFN3) APPROVED** (user, 2026-11-15 12:54).
  **DENOISE-ONLY-SOURCE RULE**: denoise ONLY the source video's own audio
  FIRST; SFX mixed AFTER, never through the denoiser; never denoise a
  finished mix; never chain DFN with anlmdn/afftdn; no `--pf` unless asked.
  (See `03-audio-and-voice.md`.)
- **KEY-POINTS-ONLY RULE** (user, 2026-11-16 08:56):
  "হোলসেল ভিডিওগুলোর ক্ষেত্রে সব সাবটাইটেল দিতে হবেনা। শুধু কি-পয়েন্ট গুলো
  সুন্দর করে দিবা" — wholesale/sales videos get NO full subtitles, only key
  points as beautiful overlays timed to speech.
- **FULL SUBTITLES ONLY FOR BRAND BEATS** (user, 2026-11-16 08:57).
  Full-text subtitles stay ONLY in Brand Beats videos.
- **B-ROLL TEXTURE ZOOM** (user, 2026-11-16 08:56): B-roll photos must be
  shown ZOOMED IN so fabric texture (weave, jacquard, embroidery, buttons)
  is clearly visible, not only full-garment cards.
- **Key points sourced from OUR transcripts only** — the project transcripts
  including any user-edited version. Nothing invented. (User, 2026-11-16 09:37.)
- **VISIBLE-EVIDENCE RULE** (user, 2026-11-16 08:24–08:27): "ব্যাগে আর জামার
  ট্যাগে দেখা গেছে তারপরও ঠিক করো নাই কেন?" — visible on-screen evidence
  (brand names on bags/tags/signage IN the footage) OVERRIDES the
  keep-as-heard rule. Cross-check spoken names against frames.
- **SHOP SPLIT** (user, 2026-11-16 08:27): sales videos 1–2 = RIGHT CHOICE
  ("রাইট চয়েজ"); video 3 = **দুলহা পাঞ্জাবি (Dulha Panjabi)**, a different
  shop. Never mix names/addresses/phones between them.
- **SPELLING-PREDICTION RULE** (user, 2026-11-16 08:29): "তোমার তো উচ্চারিত
  শব্দগুলো প্রেডিক্ট করা উচিত ছিলো" — predict the spoken words from context
  and correct ALL phonetic ASR spellings to proper Bangla (শুন্দুর→সুন্দর,
  কলেক্সান→কালেকশন — "কালেক্সান হয় কখনো? বুঝায় তো যাচ্ছে ওটা কালেকশন";
  মেকিন্গটা→মেকিংটা — "মেকিনগটা হয়ে আছে। ওটা মেকিং হবে"). Flag ONLY
  genuinely unresolvable spans/names. Address spelling still unverified
  (no visible signage) — captions as heard, no address card, until the user
  confirms.
- **GRADE: visible + balanced** (user, 2026-11-16 08:59/09:10): video 1 v1
  was too dark → brighten, keep quality (no clipped highlights, no crushed
  blacks, no extra lossy passes); garments must NOT become over-white/washed
  out — "কাপড় যেনো বেশি সাদা না হয়" — keep cream tones + weave texture
  visible.
- **LIVE VERIFICATION** (user, 2026-11-16 09:11): Muse personally views
  actual rendered frames/clips before delivery — never deliver on
  settings/descriptions alone.

## All videos

- **NO-BLACK-BACKGROUND RULE** (user, 2026-11-15 13:55):
  "ব্যাকগ্রাউন্ডটা কালো রাখবানা কখনো। এতে ফেসবুক রিচ কমে যায়" — NEVER a
  black/dark background in any video; it reduces Facebook reach. All videos
  use a LIGHT background (cream + lime). Already-posted dark-background
  videos stay as-is unless the user orders a redo.
- **BACKGROUND FRAME** (user, 2026-11-15 13:56): "ব্যাকগ্রাউন্ডে সুন্দর ফ্রেম
  রাখবা" — the light background must carry a beautiful decorative frame,
  never a plain flat color.
- **WATERMARK** (user, 2026-11-14 00:22, refined 00:23): Brand Beats
  watermark on Brand Beats videos from the USP video onwards — SMALL and
  subtle, must never make the video look bad. Does NOT change the story
  videos' (ঢেউ/তাকবির, Saimstory content) no-watermark rule.
- **NO-COPIED-NAMES RULE** (user, 2026-11-12 23:09): "আগের ভিডিওতে যে
  নামগুলো আছে সেগুলো দিও না। কপি বলবে" — mock UI in videos must NEVER reuse
  names/details from the reference video. BANNED strings: Meghna Attire,
  Sakib Rahman, Nusrat Jahan, Navy Panjabi / নেভি পাঞ্জাবি, ৳2,250, PJ2101,
  M/L/XL size line. Mock chats/inbox/bills use NO personal names and NO shop
  names — generic "কাস্টমার" labels only; any product/price/code shown must
  be invented and clearly different from the reference. (Does NOT apply to
  intrinsic story names in story videos, e.g. Rahim Chacha.)
- **FOOTAGE RULE** (user, 2026-11-14): "বাট ফটো, ভিডিও ইউজ করবা নেক্সট থেকে"
  — from the next videos onwards, USE photos + video footage. "ফটো, ভিডিও
  ফুটেজ গুলো ক্যারোজেল কার্ডের মতো মোশন গ্রাফিক্স হিসেবে ভিডিওতে আসবে" —
  photos/footage enter as CAROUSEL-CARD style motion graphics.
- **ITEM-MATCH RULE** (user, 2026-11-14 13:20): opening narration said
  blazer/suit but hangers showed shirts — fix next time, small mistakes must
  not remain. Footage must show the EXACT item the narration names.
- **LOCATION RULE** (user, 2026-11-14 11:44): "নেক্সট টাইম লোকেশন ঠিক রাখবা।
  দোকানের বাইরে বললে দোকানের বাইরের ফুটেজই" — footage location must match
  the narration.
- **DETAILED B-ROLL RULE** (user, 2026-11-14 10:15): "B-roll সবগুলোরই
  ডিটেইল্ড দিবা" — detailed, script-matched B-roll in ALL videos. Scenes
  follow the narration's action beats.
- **VOICE = ELEVENLABS RAHAT NARRATOR FOR ALL VIDEOS** (user, 2026-11-12
  22:50–22:53, supersedes Poulomi): "ELeven Labs দিয়ে করবা এরপর থেকে। Rahat
  Narrator এর ভয়েস এটা। জোশ" — from now on use ElevenLabs 'Rahat -
  Narrator' for ALL videos; the user provides the audio files. English
  versions use the Melody voice.
- **SCRIPT ADAPTATION RULE** (user, 2026-11-14 09:59): "এটা আমাদের স্ক্রিপ্ট
  লেখার টিপস। এভাবে করবা" — localize setting/character/currency/amounts/
  mascot, renumber from Day 1, remove source branding, keep structure +
  lesson. (See `07-brand-beats-videos.md`.)
- **BRANDING RULE** (user, 2026-11-14 13:40): "এবার দেখে বল্টু দি গ্রেট
  বলবোনা। আমাদের নিজেদের ব্র্যান্ডিং করবো। Brand Beats এর সিইও বলেন-" —
  DROP বল্টু দি গ্রেট স্যার / Professor Max from all future scripts/builds;
  the expert line is "Brand Beats এর সিইও বলেন-" / "The CEO of Brand Beats
  says-".
- **DAY-COUNT RULE** (user, 2026-11-14 13:45): "আর এটা ডে ৩ বলবানা। ডে১ ই
  থাকবে। তুমি হিসাব করে রাখবা কতো তম দিন, তার উপর বেইজ করে দিবা নেক্সট থেকে"
  — day number = calendar day of the run (Nov 14 = Day 1), not video
  sequence; Muse tracks and assigns. (Threshold-gap kept Day 3 by a later
  same-day decision: "এই ভিডিওটা Day 3 ই থাকুক" — the rule applies from the
  next video onward.)
- **USER CLAIMS — VERIFY FROM THE ORIGINAL SOURCE FIRST** (user, 2026-11-13
  23:03): "যেটা বলি আগে যাচাই করবা অরিজিনাল সোর্স থেকে। তারপর বলবা" — when
  the user states a platform/product fact, check the ORIGINAL source before
  replying or asserting anything. A correction from the user is a
  verification task, not a debate.
- **Study the reference exhaustively first; lay out the understanding for
  approval before building.** Show a photo first and a video on request.
  Self-verify the rendered result repeatedly before handoff. A red-marked
  screenshot or a Bangla position direction is the final spec.
  (Standing practice.)
- **SFX FOLLOW THE SPOKEN WORDS** (story videos; user, 2026-11-13 08:56):
  "যে কথা গুলো থাকবে সেই কথাগুলোর উপর ভিত্তি করে সাউন্ড ইফেক্ট হবে।
  নাম্বারস, গ্রাফ, বেল, নক এগুলোর জন্য এক্সট্রা সাউন্ড ইফেক্ট থাকে
  স্টোরিলাইনের উপর বেইজ করে বসাইতে হয়" — numbers/graphs/bell/knock get
  extra storyline-based SFX; counters/stat cards get supporting story-world
  sounds tied to the spoken word, never generic UI pops.
- **Be honest about limits.** No invented resolution: "Super HD" means the
  cleanest, crispest, best-graded version of what was shot — not a
  professional-camera reshoot. No filter or CPU-feasible model here
  deblurs, recovers clipped highlights, or adds true detail.

## Product showcase / rail (ORZR demo)

- **Rail is opt-in per product.** Merchants specifically choose which
  products appear on the rail showcase; NOT all uploaded products go on
  the rail. (User, 2026-11-04.)
- **Background auto-removal is mandatory** for rail products — transparent
  background, no exceptions. (User, 2026-11-04.)
- **AI hanger generation:** if the merchant's photo doesn't show the product
  hanging on a hanger, use AI to generate a hanger-hanging version (product
  on hanger, background removed, hook-tip normalized).
  (User, 2026-11-04.)
- **The hanger + wire hook must NOT be a code-drawn SVG** — merchants upload
  photos with the hanger (or AI generates them). (User, 2026-11-05.)
- **NEVER draw the hook — preserve the photo's hook in background removal**
  (user, 2026-11-05): "তুমি লাগাইতে যাচ্ছো কেন!! ব্যাকগ্রাউন্ড রিমুভ করার
  সময় হুক রিমুভ করবেনা এমন কিছু করো" — the hook must survive background
  removal. Fix: rembg **isnet-general-use**, not u2net (u2net eats the thin
  wire hook).
- **Motion blur OFF on the rail.** (User, 2026-11-05: "Motion blur এটাতে
  বন্ধ করো".) Page transitions keep their blur; the rail itself does not.

## Photos (see also 09-photos-and-broll.md)

- **Muse image generation DROPPED for styled photos** (user, 2026-11-16
  01:26): "না বাদ দাও। তোমার ইমেজ জেনারেশন মডেল ভালো না" — do not generate
  or composite styled photos again unless he orders it. The user generates
  styled photos himself in the Gemini app (Nano Banana); Muse cannot call
  the Gemini image API (0 free-tier quota, billing off).
- **Keep the hanger-hung photo look, CREAM background, fix colors,
  CONSISTENT exposure** (user, 2026-11-15 23:26, rejecting the off-white
  batch): "বাজে এডিট হইছে। হ্যাঙ্গারে ঝুলানো ফটোই থাকবে কিন্তু ক্রিম
  ব্যাকগ্রাউন্ডে আর কালার ঠিক করার। কিছু বেশি ডার্ক আর কিছু বেশি লাইট হয়ে
  আছে".
