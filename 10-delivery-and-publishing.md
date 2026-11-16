# 10 — Delivery and publishing

## Delivery routes

### Google Drive is the standing route for full-quality files

- **Chat downloads FAIL for this user at ~165 MB+.** The 237 MB v1, the
  248 MB v3, and a 248 MB interview video all failed to download from chat.
- **Muse built-in storage rejects ≥237 MB (HTTP 413).** 50 MB uploads work;
  the cap is below 237 MB. Storage links expire (a 50.5 MB compressed copy
  link expired 2026-11-17 09:12 +06). Mention expiry + anyone-with-link
  access when sharing storage links.
- **The user rejected the compressed copy and demanded the big file:**
  "বড় ফাইলটাই লাগবে। লো রেজুলেশনের না" (2026-11-15 12:00). Drive upload of
  the full-quality v3 (247,884,833 bytes) at 12:03 solved it. Full-quality
  files go via the user's Google Drive. Never invent Drive IDs/URLs.
- Upload command (Google Drive connector CLI):
  `drive files create --params '{"ignoreDefaultVisibility":true,"fields":"id,name,mimeType,size,webViewLink"}' --json '{"name":"...","mimeType":"video/mp4"}' --upload /absolute/path`
- Download command: `drive files get --params '{"fileId":"...","alt":"media"}' -o /path`
  (the `files download` command returns only a URI + 0-byte file).
- Verify the Drive account via `drive about get` + file owners — **never
  guess account emails**. The connected Drive account is
  shaidulaivid@gmail.com (verified). A browser session once invented
  kmenterprisebdsr@gmail.com — Google says it does not exist; never use it.
- `drive files trash` is NOT a valid subcommand — find the right
  delete/update command when trashing duplicates.

### New filename per version (hard rule)

Deliver EVERY video version under a NEW, distinct filename (e.g.
`name-v2.mp4`, `name-v3.mp4`); never overwrite-and-resend the same path —
the user's app serves cached old copies (see `05-lessons-and-failures.md`
§42). The user explicitly asks for a new file each time.

### Verification before delivery

- Parent views actual rendered frames/clips before delivery (LIVE
  VERIFICATION rule) — never deliver on settings/descriptions alone.
- Loudness measured on the FINAL file (ffprobe + ebur128). md5 + byte size
  recorded. Frame QA: 2 fps sweep ALL viewed + 10 fps dense on card spans +
  per-phrase caption crops + per-card frames (see
  `04-technical-pipeline.md`).
- Honest gaps disclosed at delivery (e.g. uncaptioned spans, approximate
  timing regions, buried-cue counts, treatments that stand in for missing
  footage). Completion claims tightly scoped: always name what remains.
- The user is the final ear on all audio (Muse cannot hear) and the final
  eye on grade/taste.

## Publishing

### Standing position

- **No posting anywhere unless the user orders it**, with the exact copy +
  destination approved. No GitHub push for video work except this training
  repo (user order, push only when he is online).
- The KM Enterprise publish below was an explicit one-time exception to the
  no-posting rule in that chat.

### Business Suite browser route (KM Enterprise video 2, 2026-11-15)

- Order (19:34): publish video 2 to the **KM Enterprise Facebook Page from
  his own ID**. Facebook connector NOT connected; Accounts Center was
  BLOCKED 2026-11-12. Route = Business Suite browser with saved
  facebook.com login.
- **Browser input-file size limit:** `browser.browse` `files` rejects large
  files (423 MB → "exceed the classification size limit"). Workaround:
  upload to Drive first, browser downloads from the Drive link. The file
  was set to anyone-with-link (reader) at 19:58 because the connected Drive
  account is NOT any of the browser chooser accounts (signed-in download
  fails with "You need access"). **REVERT the link-sharing to private**
  once the publish is confirmed done (still owed).
- Composer reached: Page verified **KM Enterprise (Page ID
  1354066851120193)**, caption pasted verbatim, story sharing off, Public;
  video download verified complete. Blocker: native OS file picker cannot
  be driven by browser automation; takeover request (20:13) unanswered;
  task errored 22:13. **Verified 22:15: NOT published.** A TEXT-ONLY draft
  exists, no video (business_content_id **2181835492691943**, updated
  20:09, caption intact) — warn the user it could cause a duplicate if he
  uploads fresh.
- **User chose self-publish (22:42)**: "ক্যাপশন দাও। আমি আপলোড করতেছি" —
  exact caption + Drive link delivered. No confirmation received yet that
  he published.

### Caption rules (user, 2026-11-15 19:36)

- Target wholesale customers, Facebook algorithm friendly, **NO DASHES of
  any kind** ("C-62" must not appear → "দোকান নং 62").
- **Approved caption (verbatim):**

> পাইকারি দামে জিন্স প্যান্ট নিতে চান?
> দোকানের জন্য স্টক খুঁজছেন? কেএম এন্টারপ্রাইজে পাবেন নানা ডিজাইনের ডেনিম
> জিন্স, সরাসরি পাইকারি দামে। নানা সাইজ available, পাইকারি বিক্রি হয়।
>
> অর্ডার করতে কল করুন অথবা ইনবক্সে মেসেজ দিন।
> 📍 ঠিকানা: মিরপুর ১ নাম্বার, শাহ আলী কলেজ মার্কেট, দ্বিতীয় তলা, দোকান নং 62
> 📞 ফোন: 01834 963 786
>
> কমেন্টে জানান, আপনার দোকানের জন্য কোন সাইজটা বেশি চলে?
>
> #পাইকারি #জিন্সপ্যান্ট #ডেনিম #wholesale #KMEnterprise

### Brand Beats posting (masterclass series)

- Identity gate: verify Page name AND post URL id= before posting (the
  test-page trap: "Brand Beats" vs "Brand Beats test AI" — see
  `05-lessons-and-failures.md` §52). Post to Brand Beats /
  brandbeats.agency. No first comment unless ordered.
- Caption + 8 hashtags pattern. English versions to LinkedIn + Pinterest on
  user order only. Posting records (IDs, times) live in
  `07-brand-beats-videos.md`.

### Cloudflare / tracking (docs-only, blocked)

- Cloudflare setup is blocked from the browser and network by Turnstile
  with no puzzle; the user himself tried twice and failed. The tracking
  setup guide is docs-only with live checks and screenshots still owed.
  (Not a video rule — recorded so nobody re-attempts the blocked route
  expecting it to work.)
