# Legend Earn

Landing page for Legend's onchain earning product. Static HTML, zero build step, pixel-matched to Figma at 1440px with mobile responsive fallback.

**Repo:** [github.com/monodexr/action-earn](https://github.com/monodexr/action-earn)

## Quick Start

```bash
git clone https://github.com/monodexr/action-earn.git
cd action-earn
python3 -m http.server 8090
# Open http://localhost:8090
```

No Node, no npm, no build. One HTML file + assets.

To share a public URL:

```bash
cloudflared tunnel --url http://localhost:8090
```

## Editing Copy

All page text is documented in `COPY.md` with unique keys per string. Edit the values, then hand the file to an engineer (or AI agent) to apply changes to `index.html`. The key format maps 1:1 to the HTML.

## Project Structure

```
action-earn/
├── index.html            # Single-file app (markup + styles + scripts)
├── COPY.md               # Editable copy document — all page text with keys
├── HANDOFF.md            # Figma coordinate spec — (x, y, w, h) for every element
├── README.md
│
├── fonts/
│   ├── Knapp-Light.woff2
│   ├── Knapp-Regular.woff2
│   ├── Knapp-Medium.woff2
│   ├── Knapp-Bold.woff2
│   └── ABCDiatypeMono-Regular.woff2
│
└── images/
    ├── hero-bg.png           Hero poster fallback (3840x2160)
    ├── hero-video.mp4        Hero background video loop
    ├── earn-video.mp4        Section 2 phone UI video
    ├── earn-video.mov        Safari fallback for Section 2 video
    ├── footer-bg.png         Landscape + logo with alpha (5760x3087 RGBA)
    ├── spot01.png             Card 1: USDC + bank + QR
    ├── spot02.png             Card 2: Compound migration
    ├── spot03.png             Card 3: USDC→ETH trade
    ├── spot04.png             Card 4: token cascade
    ├── usdc-aave.png          Token: USDC + Aave
    ├── usdc-morpho.png        Token: USDC + Morpho
    ├── eth-morpho.png         Token: ETH + Morpho
    ├── eth-compound.png       Token: ETH + Compound
    ├── usdt-optomosm.png      Token: USDT + Optimism
    ├── usdh-hyperevm.png      Token: USDH + HyperEVM
    ├── logo-full.svg          Mark + wordmark
    ├── logo-mark.svg          Mark only
    ├── corner-tl.svg          L-bracket (CSS-rotated for 4 orientations)
    ├── earn-icon.svg          Green bar chart badge
    ├── action-icon.svg        Green earning badge
    ├── app-store.svg          App Store badge
    ├── apple-icon.svg         Apple logo (white)
    ├── menu-icon.svg          Hamburger
    ├── morpho-logo.svg        Morpho wordmark
    ├── compound-logo.svg      Compound wordmark
    ├── aave-logo.svg          Aave wordmark
    ├── social-farcaster.svg   Social icon
    ├── social-x.svg           Social icon
    └── social-linkedin.svg    Social icon
```

## Page Sections

| # | Section | Desktop Height | Description |
|---|---------|---------------|-------------|
| 1 | Hero | 880px | Background video, frosted nav bar, rate headline, powered-by logos |
| 2 | Real-Time Interest | 779px | Looping phone UI video in rounded card with corner brackets |
| 3 | Rates | 926px | Animated horizontal bar chart comparing rates (4 bars, fixed px widths) |
| 4 | Features | 1700px | 2x2 card grid with spot illustrations and numbered labels (01-04) |
| 5 | Markets | 920px | Animated counters, asset filters, 4x2 market card grid |
| 6 | Comparison | 920px | 7-row data table vs 6 competitors with hover highlights |
| 7 | FAQ | Auto | Dark section, 6-item accordion (first open by default) |
| 8 | Footer | 1180px | RGBA landscape bg with alpha fade, links, CTA, social icons |

## Design System

### Typography

| Font | Weight | Tailwind | Usage |
|------|--------|----------|-------|
| Knapp | 500 (Medium) | `font-knapp font-medium` | Headings, primary body |
| Knapp | 400 (Regular) | `font-knapp` | Secondary body text |
| ABC Diatype Mono | 400 | `font-mono` | Labels, decorators, metadata |

### Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `light` | `#f8f8f8` | Page background |
| `dark` | `#131313` | FAQ + footer background |
| `text-1` | `#2e2e2e` | Primary text |
| `grey-800` | `#6c6c6c` | Secondary text |
| `grey-700` | `#949494` | Tertiary text |
| `grey-600` | `#b2b2b2` | Muted / large body text |
| `green` | `#008500` | Accent color (rates, badges) |
| `text-2` | `rgba(46,46,46,0.6)` | Comparison table secondary |
| `text-3` | `rgba(46,46,46,0.4)` | Comparison table FPO values |

### Layout Grid (1440px)

Three vertical dashed lines at absolute page x-coordinates:

| Line | x | From grid container |
|------|---|-------------------|
| Left | 32px | `left: 0` |
| Center | 490px | `left: 458px` |
| Right | 1408px | `right: 0` |

Content sits in two columns:
- **Left column** (32px - 458px): Section headings + decorator labels
- **Right column** (490px+): Body copy, charts, cards, tables, grids

### Corner Brackets

Single SVG (`corner-tl.svg`) rotated via CSS transforms. The default shape is `┌` (horizontal right, vertical down).

| Position | Transform | Result |
|----------|-----------|--------|
| Top-left | `scaleX(-1)` | `┐` points inward |
| Top-right | none | `┌` points inward |
| Bottom-left | `scale(-1)` | `└` points inward |
| Bottom-right | `scaleY(-1)` | `┘` points inward |

### Decorator Pattern

Each section heading has a mono-caps label (RATES, FEATURES, MARKETS, COMPARISON, FAQ) that sits within the heading's first line. The decorator is absolutely positioned at the section's left edge with the heading using `text-indent` to push past it.

## Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| Tailwind CSS | CDN (runtime) | Utility classes, no build |
| GSAP | 3.12.5 | Scroll animations, counters, parallax |
| ScrollTrigger | 3.12.5 | Scroll-triggered reveals and bar chart |
| Vanilla JS | - | FAQ accordion, nav, filters, hover effects |

## Animations

| What | Trigger | How |
|------|---------|-----|
| Section elements fade up | Scroll to 88% viewport | GSAP + ScrollTrigger |
| Hero text fade in | Page load + 0.3s | GSAP |
| Bar chart bars grow | First scroll into view | GSAP (width tween) |
| Stat counters (33, 7, $29.7B) | Scroll into view | GSAP (value tween) |
| Hero video parallax | Scroll scrub | GSAP ScrollTrigger |
| Rate ticker (7.14% +/- 0.01) | Every 3 seconds | `setInterval` |
| FAQ open/close | Click | CSS `max-height` transition |

## Responsive

- **Desktop (>=1024px):** Pixel-perfect absolute positioning from Figma coordinates
- **Mobile (<1024px):** CSS media query converts all sections to flow layout. Cards stack single-column, comparison table scrolls horizontally, font sizes reduce, grid lines hidden.

## Browser Support

| Browser | Notes |
|---------|-------|
| Chrome / Edge | Full support |
| Safari 15+ | `playsinline` videos, `-webkit-backdrop-filter`, `svh` with `vh` fallback |
| Firefox | Full support |
| iOS Safari | Autoplay muted videos work with `playsinline` |

## Deployment

Zero-config static deploy. No build command needed.

```bash
# Vercel
npx vercel --prod

# Netlify
netlify deploy --prod --dir .

# GitHub Pages
# Settings → Pages → main branch → / (root)

# Cloudflare Pages
# Connect repo, no build command, output: /
```

## Key Files for Engineers

| File | Purpose |
|------|---------|
| `index.html` | The entire site. Edit this. |
| `COPY.md` | All text content with keys. Edit copy here, apply to HTML. |
| `HANDOFF.md` | Figma coordinate reference. Every element's (x, y, w, h). |

## Figma Source

[figma.com/design/PPbPvXwLy0OKZmQCTFwmoI/Diagrams?node-id=4405-40662](https://www.figma.com/design/PPbPvXwLy0OKZmQCTFwmoI/Diagrams?node-id=4405-40662)
