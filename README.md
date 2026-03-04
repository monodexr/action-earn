# Legend Earn — Landing Page

A pixel-accurate landing page for Legend's DeFi earning product, built from Figma design specs at 1440px with mobile responsive fallback.

**Live preview:** Run locally or deploy to any static host (Vercel, Netlify, Cloudflare Pages, GitHub Pages).

## Quick Start

```bash
# Clone and serve
git clone <repo-url> && cd action-earn
python3 -m http.server 8090

# Open http://localhost:8090
```

No build step. No dependencies. No framework. One HTML file, custom fonts, and image assets.

For a shareable tunnel URL:

```bash
cloudflared tunnel --url http://localhost:8090
```

## Project Structure

```
.
├── index.html              # Everything — markup, styles, scripts
├── fonts/
│   ├── Knapp-Light.woff2
│   ├── Knapp-Regular.woff2
│   ├── Knapp-Medium.woff2
│   ├── Knapp-Bold.woff2
│   └── ABCDiatypeMono-Regular.woff2
├── images/
│   ├── hero-bg.png         # Hero poster (3840×2160)
│   ├── hero-video.mp4      # Hero background video (1280×720, 21s loop)
│   ├── earn-video.mp4      # Section 2 phone UI video (looping)
│   ├── earn-video.mov      # Safari fallback
│   ├── footer-bg.png       # Composited landscape + logo + gradient
│   ├── phone-screen.png    # App screenshot (unused, replaced by video)
│   ├── spot01–04.png       # Feature card illustrations
│   ├── usdc-*.png          # Token icons (USDC + protocol badge)
│   ├── eth-*.png           # Token icons (ETH + protocol badge)
│   ├── usdh-hyperevm.png   # Token icon
│   ├── usdt-optomosm.png   # Token icon
│   ├── logo-full.svg       # Legend mark + wordmark
│   ├── logo-mark.svg       # Legend mark only
│   ├── corner-tl.svg       # L-bracket decorator (rotated via CSS for all 4 corners)
│   ├── social-*.svg        # Farcaster, X, LinkedIn icons
│   └── ...                 # Other SVG icons and logos
├── HANDOFF.md              # Original Figma coordinate spec (for reference)
└── README.md               # You are here
```

## Page Sections

| # | Section | Height | Key Elements |
|---|---------|--------|-------------|
| 1 | **Hero** | 880px | Background video, frosted nav, "Earn up to 14.89%", powered-by logos |
| 2 | **Real-time Compounding** | 779px | Looping phone UI video in rounded card with corner brackets |
| 3 | **Capture the Yield** | 926px | Animated horizontal bar chart (4 bars, fixed pixel widths) |
| 4 | **Features** | 1700px | 2×2 card grid with spot illustrations and numbered labels |
| 5 | **Real Markets** | 920px | Counter animations, asset filters, 4×2 market grid |
| 6 | **Comparison** | 920px | 7-row table with 6 competitors, hover highlights |
| 7 | **FAQ** | Auto | Dark section, 6-item accordion (first open by default) |
| 8 | **Footer** | 1180px | Nature landscape BG, links, CTA, social icons |

## Design System

### Fonts

| Font | Weight | Usage |
|------|--------|-------|
| Knapp Medium (500) | Headings, primary body | `font-knapp font-medium` |
| Knapp Regular (400) | Secondary body | `font-knapp` |
| ABC Diatype Mono (400) | Labels, metadata, decorators | `font-mono` |

### Colors

| Token | Value | Usage |
|-------|-------|-------|
| `light` | `#f8f8f8` | Page background |
| `dark` | `#131313` | Dark sections (FAQ, footer) |
| `text-1` | `#2e2e2e` | Primary text |
| `grey-800` | `#6c6c6c` | Secondary text |
| `grey-700` | `#949494` | Tertiary text |
| `grey-600` | `#b2b2b2` | Muted text |
| `green` | `#008500` | Accent (rates, earn badge) |

### Grid

Three vertical dashed lines at page x-coordinates `32`, `490`, and `1408`. Content lives in two columns:

- **Left** (32–458px): Section headings + decorators
- **Right** (490px+): Body copy, charts, cards, tables

### Decorator Pattern

Each section heading has a mono-caps label (RATES, FEATURES, etc.) positioned at the start of the heading's first line using `text-indent`. The decorator sits absolutely at the section's left edge, sharing vertical space with the heading.

### Corner Brackets

One SVG (`corner-tl.svg`) rotated via CSS transforms for all 4 orientations:

```css
/* Top-left */     transform: none
/* Top-right */    transform: scaleX(-1)
/* Bottom-left */  transform: scaleY(-1)
/* Bottom-right */ transform: scale(-1)
```

## Tech Stack

- **Tailwind CSS** via CDN (runtime config, no build)
- **GSAP + ScrollTrigger** for scroll-triggered reveals, bar chart animations, counter animations, parallax
- **Vanilla JS** for FAQ accordion, nav scroll behavior, asset filter toggles, comparison row hover

## Animations

| Animation | Trigger | Library |
|-----------|---------|---------|
| Element fade-up reveal | Scroll into 88% viewport | GSAP ScrollTrigger |
| Hero text fade-in | Page load (0.3s delay) | GSAP |
| Bar chart width grow | Scroll into view (once) | GSAP |
| Counter 0→33, 0→7, $0→$29.7B | Scroll into view | GSAP |
| Hero video parallax | Scroll (scrub) | GSAP ScrollTrigger |
| Rate ticker (14.89% ± 0.01) | 3s interval | Vanilla JS |
| Phone float | Continuous (6s ease-in-out) | CSS keyframes |
| FAQ accordion open/close | Click | CSS transitions |

## Responsive Behavior

- **Desktop (1024px+):** Absolute positioning with exact Figma pixel coordinates
- **Mobile (<1024px):** Flow layout via `@media` block with `!important` overrides on inline styles. Sections stack vertically, cards go single-column, comparison table scrolls horizontally, font sizes reduce.

## Browser Support

- Chrome/Edge (latest)
- Safari 15+ (video `playsinline`, `-webkit-backdrop-filter`, `svh` with `vh` fallback)
- Firefox (latest)
- iOS Safari (tested with `playsinline` for autoplay video)

## Deployment

This is a static site. Deploy anywhere:

```bash
# Vercel
npx vercel --prod

# Netlify
netlify deploy --prod --dir .

# GitHub Pages
# Push to repo, enable Pages from Settings → main branch → / (root)

# Cloudflare Pages
# Connect repo, build command: (none), output directory: /
```

## Figma Source

Design file: `https://www.figma.com/design/PPbPvXwLy0OKZmQCTFwmoI/Diagrams?node-id=4405-40662`

See `HANDOFF.md` for the complete coordinate map with exact (x, y, w, h) for every element across all 8 sections.
