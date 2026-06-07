# Final polish pass

Reviewed 13 fresh viewport-size screenshots (4 desktop day, 4 desktop night, 4 mobile, 1 RSVP) against the Facebook pressed-flower banner, the Wallflowers Upstairs press shoot, and Daniel Food Diary's day-mode photography. Kept it ruthless: 10 fixes that actually earn their weight.

## 1. Hero scrim — stronger at the bottom-left under text
**Issue:** On day mode, "See the cafe menu" sits on top of a strawberry shortcake; on night mode, the subtitle paragraph competes with table candles. Text shadow alone isn't enough on hi-contrast photos.
**Fix:** Layered the hero tint as `linear-gradient(170deg, transparent 30%, rgba(15,12,24,0.40) 60%, rgba(15,12,24,0.85) 100%)` plus a tighter `linear-gradient(90deg, rgba(0,0,0,0.55) 0%, transparent 60%)` from the left, giving the left third extra contrast for copy and CTAs.
**Source of authority:** UVE Wine Bar uses an asymmetric scrim with copy weighted to the dark third — same pattern.

## 2. Tagline "A cafe by day, a bar by night" — read as tagline, not headline
**Issue:** Currently `clamp(22px, 2.6vw, 30px)` italic in the gold-fill color — sits at headline weight and competes with the wordmark.
**Fix:** Reduced to `clamp(15px, 1.4vw, 18px)`, small-caps, letter-spacing 0.32em, opacity 0.85, italic kept — reads as a printed bookplate line rather than a heading.

## 3. Mobile hero wordmark — proportional scaling
**Issue:** At 390px the "Wallflowers" SVG wordmark fills nearly the full width and bumps the spaced subtitle into wrap.
**Fix:** Added a `@media (max-width: 640px)` rule that scales the SVG `viewBox` height by giving the wordmark a `max-width: 88vw` and an interior padding so the spaced "CAFE · UPSTAIRS BAR" subtitle is visible without crowding.

## 4. Menu cards — add a 4% paper-grain noise overlay
**Issue:** Day-mode menu cards read as flat cream surfaces. Brand identity is printed menus.
**Fix:** Added a `.menu-card::before` SVG-noise overlay at 4% opacity (multiply blend on day, screen blend on night), barely perceptible but you feel it on close look — the surface stops feeling like UI.

## 5. Polaroid rotations — randomized via nth-child
**Issue:** Each polaroid has a fixed inline `--rot` between -2.4° and +2.4° — looks hand-arranged but uniformly so.
**Fix:** Added 8 `nth-child` rotation rules ranging -4.2° to +3.8° applied after the inline rules; the gallery now reads as a scrapbook the owner kept rearranging, not a CMS grid.

## 6. Drop cap — tighter optical leading
**Issue:** The 6.4em illuminated G floats correctly but creates a soft gap below itself because the body line-height (1.7) is taller than the cap needs.
**Fix:** Drop cap now has `line-height: 0.78` and `padding: 0 0.12em 0 0` (was 0.04em / 0.14em), pulling the first three body lines tighter against the cap shoulder.

## 7. Eyebrow text — stronger presence
**Issue:** "A PRESSED-FLOWER SCRAPBOOK", "FROM THE CAFE · 10:00 — 18:00" etc. were `font-weight: 600` at 11px — a touch washed out in screenshots against cream.
**Fix:** Bumped to 12px, `font-weight: 700`, letter-spacing widened to 0.32em — reads as an editorial section marker rather than a UI label.

## 8. RSVP card — wax seal at the head
**Issue:** Kirby's brief asked for "wax-sealed envelope" treatment. The card has the gold border and italic "Please reserve" header, but no actual seal.
**Fix:** Added a centered dark-red wax seal SVG (the same one used on menu signature items but larger, 72px) at the top of the card, with a hand-italic "W" embossed. Adds the vintage-letter gesture.

## 9. Smart quotes & em dashes sweep
**Issue:** Mixed punctuation: some quotes are straight (`"`) some curly (`"`); some dashes are hyphens used as em dashes.
**Fix:** Swept the visible copy: pull-quotes use curly `"…"`; en-dashes for ranges (`10:00–18:00`); em-dashes for parenthetical breaks (`—`); kept HTML attribute values straight (`alt="…"`) as required by syntax.

## 10. Section ornament before press quotes — close the rhythm
**Issue:** Pressed-flower ornaments appear above Manifesto and below Menu — but not on the Press Quotes section, breaking the rhythm.
**Fix:** Added the same pressed-decor SVG above "Said in the press" — three sections now bookend with botanical ornaments, gallery and visit feel like they belong to a single edition.

## Considered and intentionally skipped

- **Replacing Cormorant Garamond** — Kirby asked if it looks "anemic on dark backgrounds." Looked at the n1 night hero: the wordmark stroke at font-weight 500 italic holds well because the stroke filter inflates it a hair. No swap needed.
- **Adding more cocktail-glow on night bar cards** — already implemented as a `::after` radial hover. Cards look right.
- **Drop cap echoing Didone** — Cormorant Garamond is a transitional serif; FB banner wordmark is script-cursive, not Didone. Sticking with Cormorant keeps brand voice intact.
- **Day↔night transition animation** — already runs a 600ms radial sweep + palette crossfade. Tasteful as-is.

## Live URL note
Vercel deploy still blocked on Kirby's expired token. The commit pushes to GitHub but won't auto-deploy until `login-then-deploy.bat` is run. Localhost serves the same code that production will, so the screenshots are accurate to the live experience once deployed.
