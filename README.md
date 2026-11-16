# Video Creation Instructions for Muse

This repository holds everything Muse has learned about creating videos for
Shahidul — every standing rule, style system, technical pipeline, lesson,
and failure, gathered from real builds and the user's own corrections.

## The living-document rule (user order, 2026-11-16)

> "ভিডিও ক্রিয়েশনের তোমার যতো ট্রেনিং আছে সেগুলো এই গিটহাবে পুশ করবা।
> প্রতিবার যা যা শিখতেছো সেগুলো আপডেট করবা"

Translation: push ALL of Muse's video-creation training to this repo, and
UPDATE it every time Muse learns something new about video creation.

That order is standing. After any video build, correction, or failure:

1. Add the new rule, lesson, or fix to the right file below.
2. Attribute it: who said it (the user, or a measured finding), the date,
   and the user's own words where he stated it. Keep his Bangla wording.
3. Record failures with three parts: what went wrong, the fix, and how the
   fix was verified. A fix without verification is not a lesson yet.
4. Never invent a rule, number, or claim. If a source cannot be read,
   record it as a gap instead of guessing.

## Index

| File | Contents |
|---|---|
| `01-standing-rules.md` | Every user-stated rule, attributed with date + verbatim quote where known. Read this first. |
| `02-style-and-editing.md` | The style guide distilled from 28 reference videos: families, rhythm, captions, transitions, motion grammar, and the 1DKM adoption notes. |
| `03-audio-and-voice.md` | Loudness standard, cue audibility, denoise (DeepFilterNet), voices, beds, SFX grammar, mix traps. |
| `04-technical-pipeline.md` | Remotion, ffmpeg, transcription, caption shaping, grading chains, rendering, QA tooling, environment limits. |
| `05-lessons-and-failures.md` | Numbered lessons: what went wrong, the fix, how it was verified. Includes the rail-demo, mobile, and environment lessons. |
| `06-wholesale-and-sales.md` | The wholesale/sales video system: KM Enterprise builds, Right Choice / Dulha Panjabi sales videos, transcript discipline, grades. |
| `07-brand-beats-videos.md` | Brand Beats masterclass + promo videos: adaptation, branding, day-count, localization, posting records. |
| `08-story-videos.md` | Long-form story videos (ঢেউ / তাকবির): the Ashik AR system, SFX rules, illustration pipeline, the dropped Takbir sound work. |
| `09-photos-and-broll.md` | Product photo work, background removal, the hanger rules, Gemini vs built-in generation verdicts, B-roll rules. |
| `10-delivery-and-publishing.md` | Delivery routes (Drive), file-size limits, the new-filename rule, browser publishing, caption rules, verification before delivery. |
| `11-sfx-inventory.md` | SFX inventory: which sounds exist, what each is for, timing/mix rules, per-video usage — and the honest record that the audio files themselves cannot be pushed through the API tools (see the banner at the top of that file). |

## How to read it

- **Rules beat habits.** Where a file below conflicts with an older note,
  the newest user-stated rule wins. Superseded rules are marked as such,
  never silently deleted — the history of *why* a rule changed is training too.
- **Evidence first.** A user correction is a verification task, not a debate:
  check the original source (official docs, the live dashboard, the server's
  own records, the footage's own frames) before asserting anything.
- **Honest limits are part of the training.** Where Muse cannot verify
  something (it cannot hear audio, cannot judge taste), the files say so
  and name the user as the final judge.

## Scope

This repo covers video creation only: editing, sound, captions, grading,
photos/B-roll for videos, rendering, QA, delivery, and publishing. Product
and deployment lessons for the Brand Beats / ORLENE apps live in `AGENTS.md`
and are included here only where they directly affect video tooling
(environment limits, image-processing dependencies, browser limits).

## Provenance

First compiled 2026-11-16 from: `AGENTS.md` lessons, the memory bank and
daily notes, `~/workspace/interview-edit/study/STYLE_GUIDE.md`,
the wholesale build notes, denoise/grading/enhancement research reports,
the sales-video build notes, the Takbir queue + study notes, and the
`video_sound_cue_audibility` / `visual_reference_study` skills. Local paths
are given throughout so any claim can be re-checked against its source.
