# Legend Earn Page — Agent Handoff Brief

## What This Is

A standalone landing page for Legend (DeFi earning product). Figma design has been extracted with exact pixel coordinates. Assets and fonts are ready. The HTML exists but has layout issues that need to be fixed by rebuilding sections to match Figma precisely.

## Figma Source

**URL:** `https://www.figma.com/design/PPbPvXwLy0OKZmQCTFwmoI/Diagrams?node-id=4405-40662`  
**File key:** `PPbPvXwLy0OKZmQCTFwmoI`  
**Node ID:** `4405-40662`

Use the Figma MCP tools (`get_screenshot`, `get_design_context`, `get_metadata`) to verify any layout details. The page is 1440px wide.

## Project Location

```
legend-earn/
├── index.html          ← Main file (needs layout fixes)
├── fonts/
│   ├── Knapp-Light.woff2
│   ├── Knapp-Regular.woff2
│   ├── Knapp-Medium.woff2
│   ├── Knapp-Bold.woff2
│   └── ABCDiatypeMono-Regular.woff2
└── images/
    ├── hero-bg.png          ← Hero poster image (3840x2160)
    ├── hero-video.mp4       ← Hero background video (1280x720, 21s loop)
    ├── phone-screen.png     ← App screenshot for Section 2
    ├── footer-bg.jpg         ← Nature landscape for footer
    ├── logo-full.svg        ← Legend mark + wordmark combined
    ├── logo-mark.svg        ← Legend mark only (for footer)
    ├── earn-icon.svg        ← Green bar chart icon
    ├── action-icon.svg      ← Green earning badge icon
    ├── apple-icon.svg       ← Apple logo (white)
    ├── app-store.svg        ← App Store badge
    ├── menu-icon.svg        ← Hamburger menu
    ├── morpho-logo.svg      ← Morpho wordmark (grey)
    ├── compound-logo.svg    ← Compound wordmark (grey)
    ├── aave-logo.svg        ← Aave wordmark (grey)
    ├── corner-tl.svg        ← Corner decorator (L-shape, top-left orientation)
    ├── spot01.png           ← Card 1 illustration (USDC + bank + QR)
    ├── spot02.png           ← Card 2 illustration (Compound migration prompt)
    ├── spot03.png           ← Card 3 illustration (USDC→ETH trade)
    ├── spot04.png           ← Card 4 illustration (token cascade)
    ├── usdc-aave.png        ← Token icon: USDC + Aave badge
    ├── usdc-morpho.png      ← Token icon: USDC + Morpho badge
    ├── eth-morpho.png       ← Token icon: ETH + Morpho badge
    ├── eth-compound.png     ← Token icon: ETH + Compound badge
    ├── usdt-optomosm.png    ← Token icon: USDT + Optimism badge
    ├── usdh-hyperevm.png    ← Token icon: USDH + HyperEVM badge
    ├── social-farcaster.svg ← Social icon (light, for dark bg)
    ├── social-x.svg         ← Social icon (light, for dark bg)
    └── social-linkedin.svg  ← Social icon (light, for dark bg)
```

## Local Dev

```bash
cd legend-earn && python3 -m http.server 8090
# Then open http://localhost:8090
```

For shareable URL: `cloudflared tunnel --url http://localhost:8090`

## Design System

### Fonts
- **Knapp** (Medium 500) — headings, body
- **Knapp** (Regular 400) — secondary body text
- **ABC Diatype Mono** (Regular 400) — labels, metadata, mono elements

### Colors
- `#f8f8f8` — page background (light)
- `#131313` — dark sections (FAQ, footer)
- `#2e2e2e` — primary text
- `#6c6c6c` — secondary text (grey-800)
- `#949494` — tertiary text (grey-700)
- `#b2b2b2` — muted text (grey-600)
- `#008500` — green accent
- `rgba(46,46,46,0.6)` — text-2
- `rgba(46,46,46,0.4)` — text-3

### Grid System (1440px page)
Three vertical dashed grid lines at page x-coordinates:
- **Left:** x:32
- **Center:** x:490 (this is the main column divider)
- **Right:** x:1408

Content lives in two columns:
- **Left column:** x:32 to x:458 (426px wide) — headings + decorators
- **Right column:** x:490+ — body copy, charts, cards, tables

### Decorator Pattern
Every section heading has a small mono-caps label (like "RATES", "FEATURES", "MARKETS") that sits WITHIN the heading's first line. The pattern is:
- Decorator: absolutely positioned at `(32, section_top + 8px)` 
- Heading: starts at `(64, section_top)` with `text-indent` large enough to push the first line past the decorator
- Both share the same vertical space — the decorator (11px) fits within the heading's line height (44px × 1.1 = 48px)

Decorator widths from Figma (determines text-indent needed):
- "RATES" = 69px → text-indent: ~40px
- "FEATURES" = 91px → text-indent: ~65px  
- "MARKETS" = 86px → text-indent: ~60px
- "COMPARISON" = 109px → text-indent: ~85px
- "FAQ" = 54px → text-indent: ~25px

### Corner Decorators
Small L-shaped brackets at corners of illustration frames. There is ONE SVG file (`corner-tl.svg`) that draws a top-left L-shape. Use CSS transforms to create all 4 orientations:
- **Top-left:** no transform
- **Top-right:** `transform: scaleX(-1)`
- **Bottom-left:** `transform: scaleY(-1)`
- **Bottom-right:** `transform: scale(-1)`

---

## Page Sections — Exact Figma Coordinates

All coordinates are ABSOLUTE from each section's top-left corner (0,0).

### Section 1: Hero
**Frame:** 1440 × 880px, background video with white gradient overlay

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Frosted nav bar | 32 | 0 | 1376 | 88 | backdrop-blur, 8% white |
| Navigation | 52 | 20 | 1336 | 48 | Fixed position |
| Left frame (Earn label + headline) | 64 | 569 | 396 | 158 | |
| — "Earn" icon + label | 68 | 569 | 72 | 26 | Green icon + "Earn" text |
| — "Earn up to 14.89%" | 64 | 607 | 396 | 120 | 60px font, green % |
| "Industry-leading rates..." | 522 | 632 | 680 | 96 | 44px, grey-600 color |
| "Earn interest every second..." | 522 | 748 | 680 | 52 | 20px, grey-800 |
| POWERED BY marquee | 66 | 768 | 394 | 32 | 50% opacity |
| White gradient rectangle | 0 | 480 | 1440 | 400 | Fades from transparent to #f8f8f8 |

**CRITICAL:** Use `top:` positioning (from section top), NOT `bottom:`. Previous code used `bottom:` which positions from the element's bottom edge, causing everything to sit too high.

### Section 2: Real-time Compounding
**Frame:** 1440 × 779px

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Icon container (green badge) | 64 | 84 | 44 | 44 | White circle bg |
| Heading "Real-time compounding." | 64 | 80 | 340 | 96 | text-indent:56px for icon |
| Body copy "No lockups..." | 522 | 89 | 680 | 78 | 20px, grey-800 |
| Visual frame (phone) | 510 | 207 | 878 | 492 | Corner decorators at edges |
| — Inner card-visual area | 522 | 219 | 854 | 468 | #ededed rounded-28px |
| — Phone mockup centered inside | | | 346 | 719 | Float animation |

### Section 3: Capture the Yield
**Frame:** 1440 × 926px

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Decorator "RATES" | 32 | 88 | 69 | 15 | |
| Heading | 64 | 80 | 406 | 96 | text-indent: 40px |
| Body copy | 520 | 80 | 680 | 142 | Two paragraphs |
| Chart frame | 490 | 302 | 878 | 544 | |
| — Bar 1 (7.63% Morpho) | 490 | 304 | bar:704 | 120 | GREEN hatched fill |
| — Bar 2 (5.00% AAVE) | 490 | 444 | bar:552 | 120 | Grey hatched fill |
| — Bar 3 (4.10% T-Bill) | 490 | 584 | bar:484 | 120 | Grey hatched fill |
| — Bar 4 (0.40% Bank) | 490 | 724 | bar:99 | 120 | Grey hatched fill |

Bar spacing: 22px between bars. Each bar row: fill on left, rate text + label on right.
Bar fills are FIXED PIXEL widths, NOT percentages.

### Section 4: Features / Platform
**Frame:** 1440 × 1700px

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Decorator "FEATURES" | 32 | 88 | 91 | 15 | |
| Heading | 64 | 80 | 406 | 96 | text-indent: 65px |
| Body copy (LARGE) | 522 | 80 | 767 | 240 | **40px font, grey-600 (#b2b2b2)** |
| Small decorator | 487 | 160 | 27 | 15 | Just a tiny dash mark |
| Card 1 (add funds) | 490 | 400 | 464 | 610 | NO border on card |
| Card 2 (best rate) | 954 | 400 | 454 | 610 | |
| Card 3 (trade) | 490 | 1010 | 464 | 610 | |
| Card 4 (compound) | 954 | 1010 | 454 | 610 | |

**Card internal layout (using Card 1 as example):**
- Visual frame: card-relative (20, 16) w:424 h:414
  - Corner decorators at the 4 corners of this frame
  - Inner card-visual (rounded #ededed): inset 12-17px from visual frame edges
  - Spot image fills the card-visual
- Decorator "01": card-relative (0, 452) — absolutely positioned
- Text frame: card-relative (20, 446) w:424
  - Heading: text-indent:56px so "01" and heading share the same line
  - Body copy: 70px below heading top (mt based on Figma y offset)

Cards have NO dashed border. The dashed lines come from the page grid, not card edges.

### Section 5: Real Markets
**Frame:** 1440 × 920px

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Decorator "MARKETS" | 32 | 80 | 86 | 15 | |
| Heading | 64 | 72 | 406 | 96 | text-indent: 60px |
| Body text (main) | 522 | 76 | 680 | 52 | 20px, grey-800 |
| Body text (sub) | 522 | 140 | 680 | 24 | 16px, grey-700 |
| Stat "33" | 522 | 208 | 191 | 66 | Counter animation |
| Stat "7" | 752 | 208 | 191 | 66 | |
| Stat "$29.7B" | 981 | 208 | 191 | 66 | |
| Asset filters | 522 | 354 | 264 | 16 | "All USDC Eth USDH USDT WLD WBTC" |
| Pagination arrows | 1281 | 354 | 95 | 16 | "< 1 of 4 >" |
| Market grid | 490 | 390 | 918 | 458 | 4×2 grid of 230×229 cells |

### Section 6: Comparison
**Frame:** 1440 × 920px, `border-radius: 0 0 40px 40px` (rounded bottom)

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Decorator "COMPARISON" | 32 | 72 | 109 | 15 | |
| Heading | 64 | 64 | 435 | 96 | text-indent: 85px |
| Body copy | 522 | 73 | 680 | 78 | 20px, grey-800 |
| Vertical divider | 455 | 40 | 1 | 389 | Dashed line |
| Table frame | 32 | 256 | 1376 | 583 | |
| — Vertical divider inside table | table+458 | 0 | 1 | full | Dashed line |
| — Header row | 0 | 0 | 1376 | 79 | Labels at (32,32) and data at (490,32) |
| — Each data row | 0 | 79+ | 1376 | 84 | Label at (32,32), data at (490,32) |

Table has 7 rows: header + APR + Compounding + Min deposit + Withdrawal + Lockups + Monthly fees.
6 data columns: Legend, Aave, Nook, Coinbase Lend, Robinhood Gold, HYSAs.
Legend column values are `font-medium text-text-1`. Others are lighter.

### Section 7: FAQ
**Frame:** Dark background (#131313), padded. Within the FAQ+Footer super-frame.

| Element | x | y (relative to FAQ content) | w | h | Notes |
|---------|---|---|---|---|-------|
| Decorator "FAQ" | 32 | 8 | 54 | 15 | Light dashed before element |
| Heading | 64 | 0 | 386 | 96 | White text (#ededed) |
| Questions frame | 487 | 0 | 921 | 718 | NOT 490, it's 487 |
| — Each FAQ item | 0 | stacked | 921 | 101 (closed) / 213 (open) | |

FAQ has 6 items. First one open by default. Plus icon rotates to X when open.

### Section 8: Footer
**Frame:** 1440 × 1180px. Background image starts at y:435.

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| "Earn anytime." text | 52 | 0 | 221 | 112 | 56px font, #ededed |
| Left decorator | 32 | 12 | 0 | 4 | Just a dashed tick |
| "From anywhere." text | 534 | 0 | 261 | 112 | 56px font, #ededed |
| Right decorator | 487 | 12 | 27 | 15 | |
| CTA button | 974 | 21 | 414 | 64 | "DOWNLOAD FOR iOS" + Apple icon |
| Company links | 52 | 245 | 62 | 87 | Careers, Contact |
| Resources links | 265 | 245 | 124 | 87 | Privacy, Terms of Service |
| Social icons | 1256 | 296 | 132 | 36 | Farcaster, X, LinkedIn |
| Horizontal divider | 32 | 356 | 1376 | 1 | Dashed white/10 |
| Info bar | 52 | 380 | 1336 | 15 | Address, email, copyright |
| Footer BG image | 0 | 435 | 1440 | 745 | Nature landscape, object-cover |
| Legend logo mark | centered | ~700 | 100 | 100 | White, glowing, over landscape |

Footer uses the BG image as a BACKGROUND with dark gradient overlay on top for text readability.

---

## Known Issues in Current Build

1. **ALL section headings:** The decorator label (RATES, FEATURES, etc.) overlaps with the heading text. The `text-indent` values need to be verified — they may need to be larger or the approach needs rethinking.

2. **Feature cards:** 
   - Should have NO dashed border box (fixed in latest but verify)
   - Corner decorators need correct orientation transforms (fixed but verify)
   - Card numbers (01-04) need to sit inline with the heading's first line via absolute positioning

3. **Bar chart:** Uses fixed pixel widths now (704, 552, 484, 99) but verify they render correctly and don't overflow.

4. **Hero:** Gradient overlay needs to make text zone solid white. Use `top:480px, height:400px` gradient matching Figma's explicit white rectangle. All text must be on z-index ABOVE the gradient.

5. **Footer:** BG image should be background of entire section, not a separate element below content.

6. **Mobile:** Currently desktop-only with absolute positioning. Needs a complete mobile pass (all absolute positions need flow-layout fallback below 1024px).

## Approach for New Agent

1. Use Figma MCP `get_screenshot` for each section to visually verify
2. Build ONE section at a time, get user approval before moving on
3. Use absolute positioning with exact Figma (x, y) coordinates for desktop
4. Every element position should come from the Figma metadata, not estimation
5. Test at exactly 1440px browser width
6. After all desktop sections match, do a mobile responsive pass
