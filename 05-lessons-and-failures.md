# 05 — Lessons and failures

Numbered lessons: what went wrong, the fix, how it was verified. Numbers in
brackets refer to the `AGENTS.md` lesson numbers where the lesson was first
recorded. A fix without verification is not a lesson yet.

## Interactive rail demo (ORZR, 2026-11-04/05)

1. **Hook is part of the hanger — one unit.** [§1] The J-hook SVG and the
   garment img must live inside the SAME rotating wrapper, pivoting at the
   hanger point. Never position the hook as a separate non-rotating element:
   when the garment tilts, the hook tilts WITH it. The user notices
   instantly if they separate.
2. **Hover-flicker trap.** [§2] If the hovered element moves/rotates away
   from the mouse on hover, `onPointerLeave` fires → hover clears → element
   moves back → `onPointerEnter` fires → infinite flicker, tilt never
   visibly applies. Fix: a separate invisible hit zone that does NOT move
   (not inside the rotating wrapper). `opacity: 0` + `pointerEvents: 'auto'`
   elements DO receive pointer events.
3. **Stacking-context blocking.** [§3] A child's z-index is relative to its
   parent. A front product's huge img blocks pointer events on a back
   product's hit zone even if the hit zone has a higher z-index. Fix:
   `pointerEvents: 'none'` on the blocking imgs; hover handled solely by hit
   zones.
4. **Hit zone placement.** [§4] Put the hit zone AFTER the tilt wrapper in
   DOM order (paints on top). Keep it small and around the hanger point
   (which doesn't move during tilt) — a full-garment hit zone gets covered
   by front products' imgs.
5. **Layout width changes break test coordinates.** [§5] Card went 50% → 75%
   → absolute mouse positions for Playwright hover tests all shifted. Always
   re-measure (`getBoundingClientRect`) after layout changes; never reuse old
   coordinates.
6. **`elementFromPoint` returns the TOPMOST element** [§6] — may be a
   blocking overlay, not the intended target. Verify with `img.src` which
   product was actually hit.
7. **Browser decomposes transforms.** [§7] `scale(s) rotate(-30deg)` may be
   reported as a matrix/`rotate(33.95deg)` (that's the rail, not a bug).
   Check the right element (0×0 wrapper vs rail div).
8. **Popup visibility ≠ screenshot visibility.** [§8] A popup at `top: -140`
   relative to a container can be in the DOM but rendered off-screen — DOM
   queries find it, screenshots don't show it. Position popups inside the
   visible card area.
9. **When the user says the angle is "opposite", just flip the sign.** [§9]
   Don't argue physics — their visual judgment of direction is the spec.
10. **Playwright `mouse.move` + React state.** [§10] Screenshots may capture
    before React re-renders. `waitForTimeout` after hover before screenshot;
    verify state via DOM query, not just pixels.
11. **"Stuck tilt" after click.** [§11] Clicking a back product slides
    products; a different hanger can end up under the stationary mouse →
    browser fires `pointerenter` → tilt sticks on the wrong product. Fix: on
    click, `setHovered(null)` + `mouseMovedSinceClick=false`; `onPointerEnter`
    only sets hover if the mouse actually moved since the click (track via
    card's `onPointerMove`).
12. **Hook counter-scale.** [§12] A child inside a scaled wrapper inherits
    the scale in BOTH size and offset. To keep a fixed-size element (the
    hook) pinned at a fixed screen offset, counter-scale by dividing its size
    AND offsets by the wrapper's scale `s` (e.g. `left: -10/s, top: -41/s,
    width: 44/s`).
13. **Rail as SVG, not rotated div.** [§13] A rotated div rail needs px
    dimensions for angle/length math — breaks when the card size differs
    from assumptions. An SVG `<line>` with `viewBox="0 0 100 100"
    preserveAspectRatio="none"` and % coordinates aligns exactly with
    %-positioned hangers at any card size. Use
    `vectorEffect="non-scaling-stroke"` for constant stroke width.
14. **Rail position is the user's visual spec.** [§14] Final: top edge
    (35%, 0%) → right edge (100%, 45%), `railY(x) = (x-35)*0.69`. Hangers
    at HX0=35% → 88%. Don't "improve" the geometry without the user's mark.
15. **Page transitions: zoom + motion blur, 1.2 s + skeleton.** [§15] All
    page changes use `bb-page-in` / `bb-page-out` keyframes, 1.2 s each,
    with stronger motion blur (16px→6px→0, scale 0.92→1). Every page open
    shows a content-shaped shimmer skeleton that fades as the zoom settles
    (~1.3 s). Timers must match the 1.2 s durations or views unmount
    mid-animation.
16. **Spotlight singles: save/restore scroll.** [§16] Opening a single view
    unmounts the long main page; going back dropped the user at the top.
    Fix: save `window.scrollY` on open, restore via double-
    `requestAnimationFrame` after the exit timeout remounts the main view.
17. **Animation timer race.** [§17] Open sets a timeout to settle the anim
    state to 'idle'; if the user hits back before it fires, the stale
    timeout clobbers the 'exit' state and the animation sticks. Fix: keep
    each timer in a ref, `clearTimeout` on every open/close.
18. **Rail scroll is a 0.3 s TIME-based tween (clothing rail ONLY).** [§37]
    The old frame-based ease felt slow whenever rAF ran below 60 fps.
    Fix: time-based tween, `RAIL_SCROLL_MS = 300`, easeOutCubic; drag
    follows the finger 1:1 (tween cancelled while dragging). Motion blur was
    added then REMOVED per user — but the user still saw blur: it was the
    DETAIL page zoom, not the rail. Fix: clean keyframes
    (`bb-page-in-clean`/`bb-page-out-clean`, scale only, no filter) for the
    DETAIL view only. Lesson: when the user says blur 'hasn't gone', check
    EVERY blur in the flow they watched. Measurement trap: in headless, rAF
    is sparse (~200ms/frame) — measure the tween itself, never round-trip
    polling.
19. **Infinity-loop rail.** [§46] Offset/target UNBOUNDED (clamps removed);
    position = `mod(i - offset + WRAP_SHIFT, n) - WRAP_SHIFT` (n≤1 guard:
    single product stays front). WRAP_SHIFT must exceed the front fade-out
    distance so a product teleports front→back only while fully invisible.
    Verified: 12 forward drags 01→…→15→02, 12 back drags back to 01, rail
    never empties.
20. **Drag ends with a phantom click.** [§34] `onPointerDown` calls
    `setPointerCapture`, so the click after a drag retargets to the
    DRAG-START hit zone — the rail jumped back after every drag. Fix:
    `dragMoved` ref — false on pointerdown, true when |dx| > 6px, and
    `handleClick` ignores the click (and resets) when set. Verify drags by
    the INFO-PANEL counter, never the hover popup's counter.
21. **Front hook curve clips at the card top edge.** [§40] The front hanger
    sits at rail y=0%, so any hook part above the rail point is clipped by
    overflow:hidden. The photo-hook approach avoids it (hook in the image,
    arc-top at the rail).
22. **Spotlight ADD TO BAG was fake.** [§32] Shoe/perfume/pants buttons only
    opened the cart drawer — they never added anything. Root cause: cart
    items were `{idx}` into CAT_PRODUCTS only, so spotlight products had no
    way to be added. Fix: cart item carries an optional snapshot
    `{name, price, imageUrl}` + resolver. Lesson: always test ADD buttons
    end-to-end (bag count + drawer contents), not just "drawer opens".
23. **Merchant → showcase price-tag bridge.** [§33] The panel Products Add
    form was a non-functional shell and the showcase used hardcoded mock
    data — a merchant's price could never reach a tag. Fix: fully controlled
    form, Save/Edit/Delete/reorder persist to localStorage `bb_products` +
    `bb-products-changed` event; demo-rack merges by NAME. Tag rule: mobile
    tag must read smaller than the product itself (measured: tag 51 px vs
    shoe 163 px at 280 px).

## Hanger / product photos (2026-11-05)

24. **Hanger belongs in the photo, not in code.** [§38] The code hook was
    REMOVED entirely. Demo images carry a wire hook drawn INTO the photo
    (PIL: stem + semicircle arc + tip, 5px #1c1a17, at the detected
    wood-apex center), canvas 700×1040 (hook arc-top y=6, wood apex y=40).
25. **Demo images must be consistent.** [§39] All 15 normalized — hanger apex
    centered at x=350, hook arc-top y=6, wood apex y=40.
26. **Hook must be FULLY there — dark wire survives isnet, light wire gets
    eaten.** [§45] isnet preserves DARK, free-standing wire hooks fully;
    light/silver thin hooks come out faint or partially eroded, bar-attached
    hooks often vanish. Fix: regenerate with a dark, clearly-visible wire
    hook (plain prompt + seed lottery — "DARK metal wire hook" in the prompt
    backfires, pulls rails). Verify by direct hook zooms of the NORM image,
    not the gen image.
27. **Hook must be ATTACHED to the wood.** [§42] The drawn hook was
    positioned at the garment bbox center, but the hanger apex is offset by
    up to 37 px; the stem ended at a faint rembg artifact, not solid wood.
    Fix: detect the solid body top (topmost row with a ≥40 px solid run) +
    its center x; remove small isolated components (<2000 px); clear
    everything above the body top; draw ONE hook with the stem going INTO
    the wood. Verified on close-up zooms.
28. **Hook is a thin metal wire, NOT a thick black extension.** [§43] The
    user: the hook "is NOT an extra extension, it is FIXED, it does not move
    at all." Fix: thin silver-grey wire hook (4 px, #8a8a8a), graceful open
    J-curve. The hook must read as the hanger's own wire.
29. **Front-view product photos: generate + bg-remove locally.** [§41]
    Pollinations flux (no key) with a negative prompt excluding people —
    without it the model adds a person/mannequin every time. rembg u2net
    with thread limits + resize to 512 px (without limits ONNX gets
    OOM-killed 137; bria-rmbg OOMs even with limits). Crop the bottom 22 px
    (watermark strip). "Blazer" strongly pulls a person — "suit jacket" +
    "empty/unworn/garment only" worked. Always verify every image on a
    contact sheet for people. Rate limit: 503 after many requests — wait
    ~45 s and retry.

## Mobile / responsive (2026-11-05)

30. **Responsive via `useIsMobile` hook** (matchMedia ≤768 px). [§18]
    Inline-style codebase → conditional styles. Breakpoint 768 covers phones
    + portrait tablets; iPad Pro 1024 gets desktop layout.
31. **Merchant panel mobile.** [§19] Sidebar → fixed overlay drawer + backdrop
    + sticky ☰ button; starts CLOSED on mobile. `minWidth: 0` on the flex
    content div is REQUIRED or tables won't scroll.
32. **Tables/grids on mobile.** [§20] Wrap in `overflowX: auto` + `minWidth`
    on inner grid; 4/5-col stat grids → 2-col or horizontal snap scroll.
33. **Spotlight grids → snap carousels.** [§21] Grids become
    `display:flex; overflow-x:auto; scroll-snap-type:x mandatory` with items
    `flex: 0 0 72-80%`.
34. **Pants carousel math is width-coupled.** [§22] Item width 360 appears in
    the translateX formula — mobile uses 220 and the formula must use the
    same variable or centering breaks.
35. **Page-level overflow hunt.** [§23] Measure
    `documentElement.scrollWidth - clientWidth` per viewport; find unclipped
    ancestors via getComputedStyle chain.
36. **Rail mobile scale.** [§26] Front garment (700 px @ scale 0.8 = 560 px)
    overflows narrow cards — apply `mobRailFactor` to tilt wrapper AND
    wire-hook call site (both must match): desktop 1, mobile ≤380 px 0.30,
    wider phones 0.45.
37. **innerWidth trap.** [§27] A mount-time `window.innerWidth` read returned
    a transient wrong value in headless emulation; `matchMedia` breakpoints
    were stable. Prefer matchMedia over innerWidth for layout decisions.
38. **Video-player crop trap.** [§28] Proof VIDEOS get zoomed/cropped by the
    user's tall-phone video player (fill mode) — the user repeatedly saw the
    dashboard's right column cut off even though the app had zero overflow.
    Static PHOTOS display fit in chat and show the true layout. For layout
    verification, send a static photo (or a tall-ratio video with content
    filling the frame); never rely on a 9:16 video alone.
39. **Record mobile videos at CSS 390 + deviceScaleFactor 2.** [§36]
    Widening the viewport to 768 px for sharpness shows the WIDE-phone layout
    — the user caught it instantly. Correct method: viewport stays 390×910
    CSS with `deviceScaleFactor: 2`; stitch the video at 1080×2520. Never
    widen the viewport for resolution.
40. **Grid min-content trap.** [§29/§31] CSS grid `repeat(2, 1fr)` is really
    `minmax(auto, 1fr)` — an unbreakable wide value forces its column wider
    and squashes the other. Fix: `repeat(2, minmax(0, 1fr))` + `minWidth: 0`
    on cards + smaller value font/padding on mobile. Always MEASURE both
    column widths after a grid fix. Full form: a table with `minWidth: 560`
    inside an `overflowX: auto` wrapper STILL grows its card — fix needs BOTH
    `minmax(0, 1fr)` on the track AND `minWidth: 0` on the item; and
    `repeat(auto-fill, minmax(300px, 1fr))` overflows phones — fix:
    `minmax(min(300px, 100%), 1fr)`. Measure the computed
    `gridTemplateColumns` when a grid overflows.
41. **Auto-fit numbers.** [§30] Dashboard stat values use a `FitValue`
    component — measures real rendered width and steps font down until it
    fits, re-fitting on resize. Verified with ৳1,23,45,67,890 at 280 px:
    shrank 20 px→13 px, overflow 0. Never let a growing number overflow its
    card — shrink the font, don't clip or wrap.

## Video builds — failures and fixes

42. **Same-path video re-sends serve STALE copies.** [§68] Sending the same
    sandbox path three times (v1, v2, v3 overwrites) made the user's app play
    a CACHED old copy — he rejected v2 and v3 without ever seeing them; the
    on-disk files were verified correct all along. The moment v3 was re-sent
    under a NEW filename, he saw the fixes. RULE: deliver EVERY video version
    under a NEW, distinct filename; never overwrite-and-resend the same path.
43. **Cue audibility must be measured against the VOICE, not the music.**
    [§60] See `03-audio-and-voice.md` — v5's cues passed at ≥6 dB over ducked
    music but sat 19–21 dB under voice peaks and were inaudible.
44. **Stacking whoosh effects is NOT sound design.** (User verdict on Takbir
    design mix, 2026-11-13.) The 399-event design mix did not close the
    complaint. Four Takbir audio passes were rejected in total (v1 soft SFX,
    v2 loud accents, v3 design mix, v4 repo mix); the user then dropped the
    work (2026-11-13 11:09). Do NOT resume Takbir sound work without explicit
    user instruction.
45. **ffmpeg QA extractions must pass `-y`.** [§70] Re-extracting over
    existing files without `-y` hangs forever on the overwrite prompt (killed
    a QA session). Always `-y` + single-pass extraction.
46. **Remotion `<Sequence>` escape bug.** [§69] See `04-technical-pipeline.md`.
    Found by QA in 2 beats, fixed by positioning all 4 card divs + spacing,
    fully re-rendered.
47. **Remotion + ffmpeg mix traps.** [§63] Concurrency 1 mandatory;
    OffthreadVideo `endAt` +1; opaque full-frame slides; mono pan bug
    (`c1=c0`); split-card framing. See `04-technical-pipeline.md`.
48. **Remotion port-probe patch mandatory.** [§62] See
    `04-technical-pipeline.md`.
49. **QA false alarms, cleared with evidence (wholesale video 1 v3):**
    (a) packet-order PTS check flagged 3830 "regressions" — packets are in
    DECODE order; B-frames make packet PTS non-monotonic (normal, not a
    defect); re-check in presentation order. (b) The "duplicated" greeting
    at 1.0–1.5 s is the deliberate `Headline` component — the v1 frame was
    BYTE-IDENTICAL, approved design. (c) ওয়াশ's "শ" looked clipped at
    80.60 s — that frame was mid bar-grow animation; the 80.78 s frame shows
    the full word + full bar. (d) `QA_EXIT:0` was `tail`'s exit code, not
    the script's — the script had failed; always check artifacts.
50. **The parent's "known differences" list was INCOMPLETE and partly wrong**
    (wholesale video 1 v3): it claimed a P19 extra "6 পিস" — verified: v1
    already read "6 পিস 6 পিস", no change. The word-by-word diff against the
    v1 backup was the authority. An intermediate শরীর→ওয়াশ fix sitting in
    render data was WRONG (user file says সুইং) and was discarded by starting
    from `v1-backup` data. Lesson: diff against the authoritative source,
    never trust a summarized differences list.
51. **Test the REAL link, never the target page directly.** [§61] An e2e that
    tested a hand-off URL against the TARGET page passed 18/18 while every
    real user was broken (the real link pointed at the bare origin, whose
    login page silently dropped the token). Rule: drive the e2e from the exact
    URL the product builds, and include a NEGATIVE CONTROL proving the
    harness can detect the old behavior.
52. **Test-Page identity trap.** [§67] TWO similar Pages exist — "Brand
    Beats" (the REAL marketing Page) and "Brand Beats test AI" (the ONLY
    Page with the webhook subscription). A re-test on the wrong Page produced
    zero webhooks/rows/replies and looked exactly like a product failure.
    Every FB test MUST verify the Page name AND the post URL's id= BEFORE
    commenting, and report both as a gate. A zero-row result with zero log
    lines means "wrong Page or no delivery" — check the post URL first.
53. **USER CLAIMS — VERIFY FROM THE ORIGINAL SOURCE FIRST.** [§66] The user
    said Business Suite does comment automation (true) and that BV shouldn't
    be needed for comment DMs (true per Meta's own doc) — both contradicted
    the standing theory, and both were right. A correction from the user is
    a verification task, not a debate.
54. **Upload approval cards offer Allow only in practice.** [§59] Every
    remote-storage upload card was decided plain "Allowed"; none ever
    recorded "Site always allowed". Never instruct the user to "choose
    always-allow"; say: approve the card within 30 minutes, and if a lasting
    option happens to show, pick it. An expired card shows nothing — a fresh
    upload must be triggered first.
55. **Page-token refresh via Explorer + server shell DOES NOT WORK.** [§65]
    The browser truncates secret values to 100 chars, paste is BLOCKED in
    the EC2 terminal, and a visually-stitched 307-char token was rejected
    malformed. The working route is the PANEL OAUTH RECONNECT by the user.
    Never plan an agent-side long-token transfer again.
56. **Browser input-file size limit.** [§76] `browser.browse` `files` rejects
    large files (423 MB mp4 failed). Workaround: upload to Drive first, have
    the browser download from the Drive link (set anyone-with-link reader
    first; verify the Drive account via `drive about get` + file owners —
    never guess account emails). Revert link-sharing after the browser has
    the file. See `10-delivery-and-publishing.md`.
57. **Chromium SIGTRAP + filesystem taint (2026-11-16).** Plain Chromium
    launches die with SIGTRAP (exit 133) — flag
    `--no-enable-multiprocess-on-linux` on every invocation. The filesystem
    taint (exec sessions lose write permission after reading pre-06:50-UTC
    files) blocked video 1 v2 at render 4/6 and video 3 v1 at render 4/10;
    resume docs carry exact commands. Recovery = VM/runtime restart or
    taint-state refresh; re-verify write-after-old-read + Chrome probes +
    pre-flight stills before resuming. Nothing needs redoing.
58. **Count-graphics warning.** On-screen text disagreed with the voiceover
    in studied reels ("49 HOMES" shown, VO says 50; "leads the bike" vs
    "hype"). Check every on-screen number/word against the VO.
59. **P26 compression (wholesale video 1).** A 5-word phrase compressed into
    0.5 s by anchor warping (0.08 s/word) — "সুইং গ্যারান্টি" flashes
    briefly; verified rendering correctly frame by frame. Compressed phrases
    render correctly but flash — flag them, don't "fix" the timing by
    inventing duration.
60. **V1 limitation that does NOT apply to v3.** The +1.75 dBTP AAC
    true-peak overshoot in wholesale video 1 v1 was fixed in v3 by the
    dynamic/TP−2 loudnorm pass + float premaster (final −14.59 LUFS /
    −1.56 dBTP). Carry limitations forward only when they still apply —
    re-measure per version.

## Environment / deploy-adjacent (affect video tooling)

61. **Dead apt mirror after VM replacement.** [§35] See
    `04-technical-pipeline.md`.
62. **Deploy image Python ≠ VM Python.** [§73] See
    `04-technical-pipeline.md`. Two build failures from verifying pins
    against the wrong Python.
63. **Sandbox DNS lies about external hosts.** [§75] See
    `04-technical-pipeline.md`.
64. **Build-first deploy sequence.** [§74] NEVER `rm` containers before a
    proven build — attempt 97's rm-before-build took the site down when the
    build failed. Sequence: (1) download + sha-verify + extract into a
    SEPARATE staging dir, copy the live .env in (600, never print),
    (2) `docker compose build` from staging (touches no running container),
    (3) STOP + delete staging + report if the build exits non-zero (site
    untouched), (4) only on build success: rm + run the deploy script.
    Attempt 98 proved the gate: build failed, site stayed 7/7 healthy.
65. **API BOOT SMOKE TEST IS MANDATORY before every deploy touching
    guards/modules.** [§55] tsc + specs NEVER instantiate the NestJS module
    graph — a missing module import crash-looped the live API while all 1333
    specs passed. Boot the real API locally (scratch DB, `/v1/health` 200,
    ZERO error lines) before deploying. (Product lesson; kept here because
    the same "tests green, boot broken" class bit video tooling verification
    too: type checks and unit tests never caught the startup failure.)
66. **Mainsite `next build` runs ESLint — tsc + vitest do NOT catch lint
    errors.** [§54] Before EVERY deploy touching mainsite files, run
    `npx eslint src` in `apps/mainsite` — 0 errors required.
67. **Spec runner staleness.** [§56] `run-a60-specs.sh` runs a STALE build
    unless rebuilt first; the spec count itself is the tell (stayed 1333
    instead of 1340). Rebuild before EVERY spec run; verify freshness by
    grepping built output + checking timestamps. A new spec must be added to
    the runner's hardcoded list or ad-hoc counts double-count.
68. **Synchronize hides entity/migration column mismatches.** [§57] Validate
    entity changes against a MIGRATION-applied schema (`synchronize: false`),
    never a synchronize boot smoke alone.
69. **Gradle daemon / Docker dead ends on this VM.** [§51] JVM loopback
    sockets are intercepted (connect accepted, write RST/dropped) — Gradle
    cannot run in any mode; Docker containers cannot start (`setns: operation
    not permitted`). EC2 build route works. A full reinstall + cache wipe
    once FIXED local builds (mechanism unproven) — retry it before declaring
    local builds dead. The sandbox policy flips with VM generations; always
    re-test loopback before promising a local build.
70. **MEMORY.md stays lean.** [§58] Per-attempt notes max 2–3 lines. When a
    tarball supersedes an older one, DROP the older tarball's facts. Condense
    superseded history in place; never leave duplicate notes.
