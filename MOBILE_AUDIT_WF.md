# Wallflowers Cafe — Mobile audit (iPhone 14: 390×844, DPR 3)

Tested via headless Chromium emulating iPhone 14 (Safari UA, touch enabled) against the live URL https://wallflower-cafe.vercel.app.

## Summary
- **No horizontal overflow.** `document.scrollWidth = 390 = viewport.width`. No bleeding elements.
- **No console errors.** Only the known `cdn.tailwindcss.com should not be used in production` warning + 1 unused-preload warning for the desktop hero size.
- **No failed network requests.** 0 × 4xx/5xx, 0 × `requestfailed`.
- **Day/night toggle WORKS on mobile.** Click on the night button flips `data-mode` and crossfades hero photos (`hero-photo--day` opacity 1→0, `hero-photo--night` 0→1).
- **Total mobile page height: 12,636px** (≈ 15 viewport heights). Within reason for an editorial single-page site, but the gallery alone is 3,983px (1-column polaroids). Halving with 2-col grid drops the page to ~10,700px.

## Bugs found

### B1 — Polaroid gallery is 1-column on mobile, ~10 viewport heights tall (HIGH PRIORITY)
`grid-template-columns: repeat(auto-fill, minmax(220px, 1fr))` on `.scrapbook` falls to 1 column at 390px width because the gutter eats most of the room. 12 polaroids × ~310px each + captions + section padding = 3,983px. Two-column would halve that.
**Fix:** Set `minmax(140px, 1fr)` for mobile via media query `@media (max-width: 640px)`, or just `grid-template-columns: repeat(2, 1fr)` for that breakpoint. Photos at ~165px wide are still legible.

### B2 — Press card "READ THE ARTICLE →" CTA is 308×31, under 44h tap minimum (HIGH PRIORITY)
4 press cards × 1 CTA each = 4 small targets.
**Fix:** Add `padding-top: 14px` (was 12) and `padding-bottom: 8px` to `.press-card__cta` so the tap surface includes the border-top spacing.

### B3 — Nav `<a>` for "Wallflowers" logo is 143×34, under 44h (HIGH PRIORITY)
Header anchor wraps daisy SVG + wordmark text. Height comes from the 34px SVG + line-height. No padding to absorb additional tap area.
**Fix:** Add `padding: 6px 0` to the header anchor.

### B4 — Footer/Visit-section in-text links 16–21px tall (MEDIUM)
- "Linktree" (40×16), "+66 94 671 4433" (107×21), "cafe@wallflowersth.com" (151×21), "094 671 4433" (76×18), "linktr.ee/wallflowersth" (142×21), social links "Instagram / Facebook / LINE / Linktree" in footer (~17px tall).
- The press-section source attribution links — "Wongnai" (50×16), "Asia Bars (Wallflowers Upstairs feature)" (338×36), "Daniel Food Diary" (99×16).
**Fix:** Apply `padding: 6px 0; display: inline-block` to these specific link clusters via a `.tap-link` class added to footer + visit-section + gallery-attribution anchors. Or scope via parent selector: footer `a`, `dd a`, `.scrapbook ~ p a`.

### B5 — "or call +66 94 671 4433" link in RSVP card is 150×20 (LOW)
The secondary "call" link below the LINE button.
**Fix:** Same `padding: 6px 0; display: inline-block`.

### B6 — Gallery section headline orphan em-dash on mobile (MEDIUM)
"Tucked away on Soi Nana — a flower shop with a cafe upstairs." wraps with the em-dash dangling at end of line 1, breaking the visual flow:
```
Tucked away on Soi Nana —
a flower shop with a cafe upstairs.
```
**Fix:** Replace ` — ` between "Nana" and "a" with ` — ` (NBSP either side of em-dash) on the day headline, AND apply same on the night headline ("A spiral staircase, candlelight, and a roof over Chinatown.") which is fine as-is — only the day one has the issue.

### B7 — Hero secondary CTA "See the cafe menu" ghost button has low contrast on mobile against the busy strawberry-cake hero photo (MEDIUM)
Day-mode ghost button blends into the cake. Night-mode equivalent ("See the bar menu") has better contrast against the candlelit interior.
**Fix:** Add a `backdrop-filter: blur(6px)` to `.btn-ghost` plus a `background: rgba(15,12,24,0.18)` when sitting over the hero (use a `.hero-ghost` class or just bump the base `.btn-ghost` slightly — won't affect dark sections meaningfully since they have border).

### B8 — Hero `<h1>` SVG wordmark on iPhone is 86vw — fine, but the spaced `CAFE · UPSTAIRS BAR` subtitle is tight at 390px (LOW)
Looking at the live screenshot, subtitle is legible but feels constrained. Acceptable as-is; leaving unfixed unless Kirby flags.

### B9 — `.menu-card` cards are visible on mobile in 1-column with full width, looking great (NO BUG)
Cards stack cleanly, gold price chips visible, wax seals on signatures, paper-curl corner present. No action needed.

### B10 — Mobile sticky CTA bar at bottom of viewport — works perfectly (NO BUG)
"Reserve a table" pill is present + readable at every scroll position. No overlap with content. No action needed.

## Not a bug — flagging for awareness
- **23 → 11 "broken images" in audit eval** — these are gallery polaroids with `data-show="day"` while toggled to night mode (or vice-versa). They have `display: none` so lazy-load doesn't fire. When the user toggles modes, the previously-hidden set starts loading. Minor UX: there's a brief blank-cell flash on toggle. Could be eliminated by switching from `display:none` to `visibility:hidden + opacity:0` so the browser pre-fetches both sets, but that doubles initial image bytes. Leaving as-is.
- **Preload warning for `wn-interior-vintage-800.webp`** — preloaded with `media="(max-width: 768px)"` but the `<picture>` `<source>` decides which size to load independently. Browser hint mismatch. Cosmetic only. Could drop one preload tag.

## Fixes being staged
B1, B2, B3, B4, B5, B6, B7. (B8 deferred, B9/B10 no-op, awareness items skipped.)
