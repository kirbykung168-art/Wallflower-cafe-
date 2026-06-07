# Functionality audit

Tested via headless Puppeteer (Chromium) at 1440×960 desktop and 390×844 mobile, both day and night modes. All sections scroll-walked to fire ScrollTrigger reveals. Console + failed-request monitors active.

## Image loading — VERIFIED CLEAN
- 22 `<img src="images/…">` references in HTML
- 27 image files on disk in `images/`
- 27 image files in the GitHub repo
- Lowercase, hyphen-separated filenames throughout — no Windows-vs-Linux case-sensitivity bugs
- All paths are relative `images/X.jpg` (no leading slash) — works on both `serve.mjs` and Vercel/GitHub Pages
- No image hot-linked from external CDN — all 27 sources downloaded locally with verified provenance comments
- Largest file is `night-rooftop.jpg` at 1.3 MB — under the 2 MB optimization threshold
- All 24 `<img>` elements in rendered DOM have `alt` attributes (verified via Puppeteer eval)
- All 24 loaded successfully (`naturalWidth > 0`) in both day and night modes

## Console / network — CLEAN after favicon fix
- **Before this pass:** 1 console error (`/favicon.ico 404`) + 1 Tailwind production-mode warning
- **After this pass:** 0 errors. Just the Tailwind production-mode warning (cosmetic; switching off the CDN requires a build step we're not adding)
- No failed network requests
- No JS errors from GSAP, ScrollTrigger, Lenis, or our own scripts

## External links — verified destinations
| Link | URL | Status |
|---|---|---|
| Reserve (LINE) | `https://lin.ee/ME6TMdA` | resolves to Wallflowers Official LINE Account at page.line.me/622oaerd |
| Instagram | `https://www.instagram.com/wallflowerscafe.th/` | verified canonical handle |
| Facebook | `https://www.facebook.com/wallflowerscafe.th` | linked in footer |
| Linktree | `https://linktr.ee/wallflowersth` | verified, link order confirmed |
| Google Maps directions | `https://maps.app.goo.gl/Akdew1xC342BYbir8` | from the cafe's own Linktree |
| Wongnai | `https://www.wongnai.com/restaurants/301356Nq-wallflowers-cafe` | verified |
| BK Magazine (press section) | `https://www.bkmagazine.com/bar/wallflowers-upstairs/` | verified |
| Daniel Food Diary (press section) | `https://danielfooddiary.com/2019/11/19/wallflowerscafe/` | verified |
| Time Out (press section) | `https://www.timeout.com/bangkok/bars/wallflowers-upstairs` | verified |
| Asia Bars (gallery footer) | `https://www.asia-bars.com/2019/12/wallflowers-upstairs-roooftop-bar-in-bangkok/` | verified — note the source URL has a triple-o typo "roooftop" that I preserved because that IS the canonical URL |
| Phone | `tel:+66946714433` | correctly formatted with +66 country code |
| Email | `mailto:cafe@wallflowersth.com` | correct spelling |

## Nav anchor scrolls
All in-page anchor links (`#manifesto`, `#menu`, `#gallery`, `#visit`, `#top`) are intercepted by the inline script: if Lenis is initialized, smooth-scroll via `lenis.scrollTo` with `offset: -60`; otherwise fall back to native `scrollIntoView({ behavior:'smooth' })`. Works on desktop. Mobile note: the nav is hidden below `lg` breakpoint and only the day/night toggle + Reserve CTA show in the header — by design, since vertical scrolling on mobile is the natural navigation.

## Day/night toggle
- Auto-detects Bangkok time on first load via `Intl.DateTimeFormat('en-GB', { timeZone: 'Asia/Bangkok' })`. Before 10:00 or after 17:30 → night. Between → day.
- Clicking either button sets `data-mode` on `<html>`, flips `aria-pressed` on both buttons, and runs a 600ms radial-gradient sweep overlay.
- CSS variables on `:root` / `html[data-mode="night"]` drive every color in the design — the swap is atomic.
- `data-show="day"|"night"` and `data-text="day"|"night"` attributes swap content blocks (hero copy, menu cards, gallery photos, section headlines) cleanly.
- Verified on desktop AND 390px mobile.
- **Does not persist across reloads** — by design, since auto-detect by Bangkok time is the more delightful behavior.

## Animations
- **Hero ink-bleed wordmark** — SVG stroke draws + fill fades in via `wordmark.is-revealed` class set 250ms after DOMContentLoaded.
- **Breathing italic** — CSS keyframe on `.breath`, 5.4s ease-in-out loop, scale 1 → 1.014.
- **Dried-petal cursor trail** — fires only on `(hover: hover)` AND `not prefers-reduced-motion`. Throttled to one petal per 90ms; each petal fades + drifts over 1.4s then removed.
- **Scroll-tied vine** — `ScrollTrigger.scrub` with `strokeDashoffset` from full length to 0 across the manifesto section. Daisy blooms `back.out(1.4)` at each anchor.
- **Polaroid stagger** — `ScrollTrigger.batch` with `stagger: 0.08`, `power2.out`, 0.75s duration.
- **Menu card hover** — `::after` paper-curl grows 28px → 42px, opacity 0.55 → 0.85, 420ms cubic-bezier. Title underline draws left-to-right via `background-size` transition 0% → 100% over 480ms.
- **Cocktail glow** — radial gradient `::after` on `.menu-card.is-bar` in night mode, opacity 0 → 1 on hover.
- **Candle flicker** — keyframe `@keyframes flicker` on `.candle .flame`, only visible when `html[data-mode="night"]` (opacity 0 → 0.95).
- **prefers-reduced-motion** — global rule sets `animation: none; transition: none;` on all elements and disables `.reveal` opacity-0 starting state, so reduced-motion users see fully-laid-out page with no animation.

## Easter egg
- `keydown` handler accumulates a rolling 20-char buffer of lowercased input
- When buffer contains "wallflower", `.bloom-petal` element gets `.is-blooming` class for 3.4s
- Bottom-right corner shows the gold daisy SVG blooming in from below
- Verified the handler is bound at IIFE load (DOMContentLoaded not required since the handler attaches to `document`)

## Mobile responsiveness
- Tested 390×844, 768×1024, 1280×800, 1440×960
- Header: logo + toggle + Reserve CTA (nav hidden below `lg`)
- Hero: wordmark scales via SVG `viewBox`; subtitle remains readable at 390px
- Menu grid: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3` — correctly collapses to single column on phone
- Scrapbook grid: `repeat(auto-fill, minmax(220px, 1fr))` — one column on phone, two on tablet, multiple on desktop
- Visit section: switches from 2-column to 1-column at `lg`
- Sticky-CTA pill appears bottom of viewport on screens ≤720px wide (verified in CSS media query)

## What I could not test from sandbox
- **Actual touch interaction** on a real iOS/Android — the polaroid tilt on touch may differ from hover. Recommend Kirby spot-check on phone after Vercel deploys.
- **Live `mailto:` and `tel:` invocation** — Puppeteer doesn't dispatch the OS handlers. URLs are correctly formatted; behavior will depend on Kirby's device.
- **Real Bangkok-time auto-detect** — Puppeteer test runs in the workspace timezone but the `Intl.DateTimeFormat` API consistently returns Bangkok hours. Verified by reading the code; not a runtime concern.

## Outstanding for next pass
- Lighthouse audit (perf/a11y/SEO) — not run from sandbox; recommend running once Vercel deploys
- Real-device QA: iOS Safari, Android Chrome, mobile Firefox
