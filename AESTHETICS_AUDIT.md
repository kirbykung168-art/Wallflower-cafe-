# Aesthetics audit

Reviewed against: the Wallflowers Facebook pressed-flower cover banner, the IG @wallflowerscafe.th identity, the vintage circular daisy logo, and the UVE Wine Bar / Schumacher House inspiration references.

## Findings & fixes

### Fixed in this pass

1. **Night hero photo was the wrong mood** — was `night-rooftop.jpg` (yellow-tinted exterior of the building from across the street). The photo read as "Bangkok street" more than "candlelit bar." **Swapped to `night-bar-interior.jpg`** — the verified Asia Bars interior shot with soft amber light, flowers and bottles — which Time Out specifically calls out as the bar's signature mood: *"Soft amber lighting is used throughout, creating a romantic yet relaxing atmosphere."*
2. **Drop cap was too small and not "illuminated"** — was a clean gold gradient at 5.2em. **Increased to 6.4em, added a 3-stop gradient (gold → brass → dried-rose), added a subtle drop-shadow halo, and a strong gold glow in night mode** so it reads as an illuminated manuscript initial.
3. **No pressed-flower decoration visible in the static layout** (only in animated petals on hero) — the FB banner's defining feature is pressed yellow-daisy + pink florals composition. **Added a new `<symbol id="pressedDecor">` SVG ornament — a thin botanical line with two leaf clusters flanking a central daisy — and placed it above the Manifesto headline and below the menu.** Echoes the FB banner directly.
4. **Menu cards looked like plain bordered boxes** — wax-seal stamps were present on Signatures, but the card body lacked the "worn paper" feel. **Added a `::after` paper-curl on the bottom-right corner that deepens on hover** (24px → 42px), giving each card the look of a printed menu page with a curled corner. Disabled on bar cards so they keep their cocktail-glow halo.
5. **Favicon 404 in DevTools console** — cosmetic but unprofessional. **Added a vintage daisy SVG favicon** (`images/favicon.svg`) matching the circular logo in the nav. Console is now clean of 404s.

### Verified as already good — left in place

- **Cafe-by-day / bar-by-night** communicates in the hero in under 1.5 seconds via the breathing "A cafe by day, a bar by night" tagline plus the day/night toggle pill.
- **Typography hierarchy** reads literary: Cormorant Garamond display + italic accents, EB Garamond body, Inter Tight for small caps eyebrows + button labels. No font fighting.
- **Color drift check**: day palette is cream/parchment with aged gold and botanical green; night is midnight-ink-violet with candle gold and dusty rose. Both match the FB banner's pressed-flower aesthetic. No off-brand defaults present.
- **Day/night transition** uses a 600ms radial-gradient sweep + 1.2s palette/photo crossfade. Not jarring.
- **Polaroid scrapbook** tilts each photo at slightly different angles with washi-tape edges + handwritten captions — the literal "pressed flowers in a scrapbook" gesture from the brief.
- **Spacing/whitespace** has room to breathe — 80px section padding desktop, 56px mobile.
- **Animations are visible without being distracting** — petal cursor trail on hover, breathing italic, candle flicker night mode, scrollTrigger reveal staggers. All respect `prefers-reduced-motion`.

### Not fixed — flagging for Kirby

- **Mobile hero wordmark** (the "Wallflowers" SVG wordmark with the "CAFE · UPSTAIRS BAR" subtitle) scales but the spaced subtitle can feel tight at 390px width. Considered a fix but the wordmark holds its proportions; the spaced letterforms are part of the editorial feel. Tell me if you want me to swap the subtitle to a non-spaced version on mobile.
- **5 unused images in `images/`** — `wn-americano.jpg`, `wn-coffee-day.jpg`, `wn-detail-1.jpg`, `wn-hero-logo-cake.jpg`, `wn-thai-style-coffee.jpg` were downloaded but never referenced. They're not broken, just dead weight. I left them in case you want to substitute them into the gallery later. ~600KB total. Want me to delete them?
- **Tailwind production-mode warning** in DevTools console (one yellow message about `cdn.tailwindcss.com should not be used in production`). Cosmetic — switching off the CDN means a build step. Left as-is; the site renders fine.
