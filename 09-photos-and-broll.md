# 09 — Photos and B-roll

## Right Choice showroom photos (25 JPGs, IMG_2210–IMG_2234)

Source: Drive folder ID `17ZGaUP3JurCfIKIhLDUgzFsoCtUl4_Om` (also held 5
videos MVI_2205–MVI_2209; MVI_2209 and MVI_2206 became sales videos 1–2;
MVI_2205/2207/2208 remain untouched, awaiting instructions). Originals:
`~/workspace/photo-grade/source/` (4000×6000 effective, EXIF-rotated).
Contents: Nehru vests (white, mint, gold, pink) + blazers (grey/blue/
off-white checks, navy), hangers in a clothing shop, warm mixed lighting;
hands/arms hold hangers in most blazer shots (2220–2234).

### Step 1 — graded batch (DONE, standing state)

Graded one by one → Drive folder "Edited Photos - 2026-11-15" (ID
`150yEDOGI11WX8wVbVo7kEPiECe47Iq6i`), 25 files, 184,427,276 bytes,
parent-verified. Local: `~/workspace/photo-grade/graded/`. This graded
batch is the current standing state of the photo work.

### Step 2 — off-white batch (DONE, then REJECTED by user)

Same FIXED OFF-WHITE background (#F7F4ED), hands removed → Drive folder
"Off-White Background Photos - 2026-11-15" (ID
`1-sghfKkfkO6c0qPgsyj6QHv-GVPFAYC6`), 25 files, 129,660,198 bytes. Local:
`~/workspace/photo-grade/offwhite/`; transparent intermediates in `cutout/`.
Method: rembg u2net (isnet kept hands/poles — rejected for this job;
bria/birefnet OOM at 6 GB). Flagged: 2213 (neck edge slightly rough at
100%) + 2234.

User rejection (2026-11-15 23:26, verbatim): "বাজে এডিট হইছে। হ্যাঙ্গারে
ঝুলানো ফটোই থাকবে কিন্তু ক্রিম ব্যাকগ্রাউন্ডে আর কালার ঠিক করার। কিছু বেশি
ডার্ক আর কিছু বেশি লাইট হয়ে আছে" — keep the hanger-hung photo look, CREAM
background, fix colors, CONSISTENT exposure.

### Cream samples (delivered 2026-11-16 00:17)

IMG_2210/2215/2230 from ORIGINALS, ONE common grade (WB R0.96/G1.00/B1.07 →
gamma 0.52 → S-curve 0.50 → sat 1.18; hangers composited WB-only so they
stay black), hangers + wire hooks restored (isnet mask + traced wire),
hands removed, fixed cream **#F6EEDD**, corners verified (245,238,220).
Local: `~/workspace/photo-grade/cream-sample/`. Nits: 2230 wire gap ~40 px
(occluded in original), 2215 shoulder smudge + wire-tip curl. Pipeline:
`~/workspace/photo-grade/work/cream/cream_build.py`.

### Reference redirect + composite sample (REJECTED with laughter)

User sent a reference image (2026-11-16 00:57): "এরকম হবে সব" — ALL photos
styled like it: cream vest on dark wooden hanger from a brass wall hook,
warm cream wall, soft window light/shadows, trailing green plant left edge,
lit lantern on wooden shelf bottom-left. A composite sample (procedural
plate + decor cropped from the reference + own black hanger kept) was built
and delivered 01:11. User laughed it off 01:13 ("কি বানাইছো এটা 🙂। তুমি
ফটো জেনারেট করতে পারোনা?") and gave his own AI prompt (verbatim below).

### The user's AI prompt (verbatim, 2026-11-16 01:13)

> Use the uploaded product photo as the exact reference for the garment.
> Preserve the vest's original design, fabric texture, jacquard pattern,
> color, collar shape, button placement, pockets, proportions, and overall
> construction. Do not redesign or alter the product.
>
> Create a premium luxury fashion product photograph of the same
> off-white/cream Nehru vest, hanging naturally on a high-quality dark
> brown wooden hanger against a clean warm off-white textured wall.
>
> The vest should be the clear hero subject, centered and fully visible
> from collar to bottom edge. Keep the garment naturally hanging with
> realistic fabric structure and subtle folds. The hanger should be elegant
> and minimal, with a premium brushed-metal hook.
>
> Use soft natural daylight coming from the upper-left side, creating
> gentle realistic shadows on the wall and subtle highlights across the
> fabric texture. The overall lighting should feel warm, refined,
> expensive, and editorial.
>
> Minimal luxury background: clean off-white wall, very subtle out-of-focus
> greenery on one side and a small warm decorative light element in the
> lower corner, both heavily blurred so they never compete with the
> product.
>
> Photorealistic, high-end South Asian menswear catalog photography,
> premium boutique aesthetic, realistic textile detail, natural shadows,
> sophisticated neutral color palette, shallow depth of field, clean
> composition, sharp product focus, realistic proportions, no people, no
> mannequin, no hands, no extra clothing, no text, no logo, no watermark.
>
> Vertical 4:5 composition, professional studio/product photography,
> premium luxury fashion campaign quality.

### AI trial → hybrid trial → DROPPED

- **AI trial** (~01:15): `media.generate_image` with the original +
  prompt verbatim → 1408×1760 webp. User ordered leaves removed from the
  front → edited version delivered. User then REJECTED (01:15): "পাঞ্জাবির
  ডিটেইলস হারায়ে গেছে। লো রেজুলেশন" — generations are 1408×1760 /
  1296×1616 vs original 6000×4000; the model redraws the jacquard pattern
  so detail softens.
- **HYBRID trial** (01:23): real garment pixels at native 4000×6000 +
  AI-generated scene (`~/workspace/photo-grade/hybrid-sample/IMG_2210-hybrid.jpg`,
  JPEG q93, 4.86 MB; pipeline `~/workspace/photo-grade/work/hybrid/build_hybrid.py`).
  Honest nit reported: garment ~65% of frame height vs reference ~75%.
- **USER VERDICT 01:26: "না বাদ দাও। তোমার ইমেজ জেনারেশন মডেল ভালো না"** —
  ALL Muse image-generation/hybrid photo work DROPPED. Do not generate or
  composite styled photos again unless he orders it.

### Gemini photos (user-generated, the B-roll sets)

The user generated the styled photos himself in the Gemini app (Nano Banana)
with his prompt: 10 vest images (01:27) + 9 blazer images (01:53) + 5
panjabi images (02:11), `Gemini_Generated_Image_*.jpg` in
`~/workspace/user/media_library/image/`, ~1856×2304 each — visibly superior.
**All 24 Gemini images are the B-roll sets for the sales videos. Never mix
the three sets** (vests → sales video 1, blazers → video 2, panjabis →
video 3).

**Gemini image API has 0 free-tier quota / billing off**, so the user
generates in the Gemini app himself; Muse cannot call it. Verified
2026-11-15: Google's official pricing page lists Free Tier "Not available"
for gemini-nano-banana-2.1, gemini-3.1-flash-image and
gemini-3.1-flash-lite-image; legacy gemini-2.5-flash-image also 0/0
paid-only (old "50/day free" claims are stale). Free image generation
exists only in consumer surfaces (Gemini app / AI Mode) — no API, cannot
drive the panel.

## Background removal

- **rembg isnet-general-use preserves the thin wire hook; u2net eats it.**
  For rail/product photos where the hook must survive: isnet. For the
  off-white batch (hands/poles must go): u2net was used because isnet kept
  hands/poles. Choose per job; verify by hook zooms.
- **bria/birefnet OOM at 6 GB** on this VM. u2net needs thread limits
  (`OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1`) + resize
  to 512 px or ONNX gets OOM-killed 137 even with free RAM.
- rembg models live in `~/.rembg/models/` (not `~/.u2net`). Proven pins
  (deploy image Python 3.11): rembg==2.0.86 + onnxruntime==1.31.1 +
  scipy==1.17.1. Plain `rembg` ships NO onnxruntime backend.
- Normalize only crops/filters/places — grep must show 0 ImageDraw in the
  normalize step (no drawn hooks). Pipeline lives in
  `~/workspace/image-pipeline/` (gen/isnet/norm/scripts + README) so it
  survives VM wipes.

## Hanger rules (summary — full lessons in 05)

- The hanger + wire hook must NOT be a code-drawn SVG; the hook must survive
  background removal; never draw/attach hooks. Dark, free-standing wire
  hooks survive isnet fully; light/silver thin hooks and bar-attached hooks
  often get eaten — regenerate with a new seed until the hook is dark +
  bar-free. The hook is a thin, fixed metal wire, part of the hanger — not
  a thick black extension, not a floating shape. Hook must be ATTACHED to
  the wood (stem goes INTO the wood).

## Generated front-view photos (Pollinations, 2026-11-05)

- Pollinations flux (image.pollinations.ai, no key) with negative_prompt =
  "person, man, woman, human, face, model, mannequin, body, wearing, worn,
  hat, people, girl, lady" — without it the model adds a person/mannequin
  every time. Prompt = "{garment} hanging on a wooden hanger, front view,
  e-commerce product photo, plain light background".
- Crop the bottom 22 px (Pollinations watermark strip). Normalize: center
  hanger at x=350, hook arc-top y=6, canvas 700×1040. "Blazer" pulls a
  person — "suit jacket" + "empty/unworn/garment only" worked. Verify every
  image on a contact sheet for people. 503 → wait ~45 s + retry.

## B-roll rules

- **Script-matched:** the picture shows what the voice is saying AT THAT
  SECOND. Random pretty B-roll is not the style.
- **Detailed:** "B-roll সবগুলোরই ডিটেইল্ড দিবা" — detailed, script-matched
  B-roll in ALL videos. Scenes follow the narration's action beats.
- **Item-match:** footage must show the EXACT item the narration names
  (blazer/suit narration + shirt hangers = failure). B-roll colours that do
  not exactly match footage garments are used ONLY at generic/quality
  moments, NEVER during color-naming.
- **Location-match:** footage location must match the narration.
- **Texture zoom (sales):** B-roll photos shown ZOOMED IN so fabric texture
  (weave, jacquard, embroidery, buttons) is clearly visible.
- **Carousel-card motion graphics:** photos/footage enter as carousel-card
  style motion graphics (footage rule).
- **Stock:** no stock VIDEO unless absolutely necessary; stock PHOTOS only
  in beautiful cards if needed (wholesale videos used zero stock).
- **Never-static:** photos must move continuously (Ken Burns acceptable
  ONLY for stills, paired with a cut every 2–4 s); B-roll must be video or
  a continuously moving photo — never a frozen still.
