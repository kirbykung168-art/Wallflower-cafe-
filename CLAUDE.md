# CLAUDE.md — Wallflowers Cafe website

## Brand
- Wallflowers Cafe · 31-33 Soi Nana, Pom Prap, Bangkok 10100
- Cafe by day (10:00–18:00) · Bar by night (17:30–00:00)
- Social proof: 92% recommend (1,294 reviews) · 33K Facebook followers · 724 posts
- Reservation link (LINE): https://lin.ee/ME6TMdA  ← PRIMARY CTA
- IG @wallflowerscafe.th · Linktree linktr.ee/wallflowersth · cafe@wallflowersth.com · 094 671 4433
- Vibe: pressed flowers · vintage · twilight · literary · gold-leaf · candlelit
- The brand is a dual identity. Day = pressed-flower parchment cafe. Night = candlelit cocktail bar.

## Always Do First
- Invoke the `frontend-design` skill before writing any frontend code.

## Local Server
- `node serve.mjs` → http://localhost:3000
- Never screenshot a `file:///` URL.

## Photo verification
- Every image MUST be confirmed as Wallflowers Cafe (cross-ref Soi Nana exterior, FB banner, IG @wallflowerscafe.th, Wongnai, RestaurantGuru, TripAdvisor).
- Inline comment in HTML next to each `<img>`: `<!-- src: <URL>, verified via <method> -->`
- If unverifiable, drop it.

## Day/Night dual identity (the centerpiece)
- `<html data-mode="day|night">`; all colors driven by CSS variables.
- Auto-detect Bangkok time (Asia/Bangkok) — if >= 17:30 default to night.
- Toggle in nav (sun ↔ moon). 600ms transition: sky gradient sweeps dusk → midnight, wordmark "blooms".
- Menu content, hero copy, hours surfaced, gallery photos all swap by mode.

## Fun interactions to ship (pick at least 4)
1. Dried-petal cursor trail on hero (desktop, respects prefers-reduced-motion)
2. Pressed-flower scrapbook gallery (tilted polaroids, washi-tape edges, handwritten captions)
3. Illuminated drop-caps on every section's opening paragraph (Cormorant + gold leaf)
4. Worn cafe-menu card treatment with wax-seal "Signature" stamp
5. Day/night transition animation (gradient sweep + wordmark bloom)
6. "Wallflowers" manifesto section — "for the quiet ones / สำหรับคนเงียบ ๆ"
7. Scroll-triggered SVG vines growing into the social-proof bar (stroke-dasharray)
8. RSVP-letter reservation card with wax-sealed LINE button
9. Easter egg: type "wallflower" → flower blooms in corner

## Typography
- Display: Cormorant Garamond (with italic + small caps)
- Body: EB Garamond (serif) or Inter Tight (sans contrast)
- Thai: Noto Serif Thai / Bai Jamjuree
- Smart quotes, en/em dashes, tight tracking on display, generous line-height on body.

## Palette
- Day:   cream `#F4ECD8`, espresso `#2C1F18`, aged gold `#B89A4A`, botanical green `#3A4A2E`, dusty rose `#C19B96`.
- Night: midnight ink `#0F0C18` (hint of violet), candle gold `#D4A84A`, deep green `#1F2A18`, rose `#B07F7C`.
- No flat colors — every surface has warmth or grain.

## Output
- Single `index.html` + `images/` + `serve.mjs` + `start-server.bat` + `vercel.json`
- Tailwind via CDN, all styles inline.
- Mobile-first. Toggle must work on mobile.

## Hard Rules
- Do not ship before screenshot round 2 (both modes, both compared to FB banner).
- Do not include any image you can't verify is this cafe.
- Do not use `transition-all`. Animate `transform` + `opacity` only.
- Do not "improve" the brand identity — match the pressed-flower / twilight / literary vibe exactly.
