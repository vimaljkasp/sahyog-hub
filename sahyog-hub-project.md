# Sahyog Hub — Project Knowledge Base

## Project Overview
The marketing/portfolio website for **Sahyog Hub**, a small digital agency founded by **Vimal** offering websites, apps, and Meta (Instagram/Facebook) ad campaigns to local businesses. Single self-contained HTML file, built to attract new clients — no frameworks, no build tools.

> **Naming history:** the brand was originally built and named **Sahyog Studio** (full brand sheet, logo, and first version of this site). It was later renamed to **Sahyog Hub** — same logo mark, colors, and tagline, just a different suffix word. All site copy and file/folder names have been updated accordingly; only the original Claude Design project (see Related Files) still carries the old "Studio" name since that's an external asset, not something this project can rename.

---

## Brand Identity
| Field | Value |
|-------|-------|
| Name | Sahyog Hub (सहयोग हब) |
| Meaning | Sahyog (सहयोग) = collaboration/cooperation |
| Tagline | "Together, we build" |
| Services line | Websites · Apps · Meta Ads |
| Founder | Vimal |
| Location | Rajasthan, India |

**Logo mark:** two facing "bracket" shapes — left bracket in Ink, right bracket in Bronze, with a small center dot in Ink. Originally sourced from a Claude Design project (`Sahyog Studio Premium Logo`, project ID `5f9ff2f5-ed87-4349-8081-0fa0f468f410`) via the DesignSync tool, back when the brand was still named "Sahyog Studio" — the mark itself is unchanged by the rename to Sahyog Hub. That brand sheet remains the source of truth for logo usage, clear space, and colour rules.

- Corner radius for app icons: 22%
- Center dot dropped below 24px icon size
- Clear space = bracket bar thickness × 4 on all sides
- Min print width 28mm / min screen width 120px

---

## Contact Details
| Channel | Value |
|---------|-------|
| Call | +91 95668 12835 |
| WhatsApp | +91 95668 12835 |
| Email | vimaljkasp@gmail.com |

---

## Design System
| Token | Value | Usage |
|-------|-------|-------|
| Ink | `#2C3040` | Primary text/logo (light mode), button bg (light mode) |
| Bronze | `#B4763C` | Accent (light mode) |
| Bronze Light | `#C9925A` | Accent (dark mode) |
| Paper | `#F7F5F1` | Background (light mode), text (dark mode) |
| Slate | `#6E7385` | Muted text (light mode) |
| Near-black | `#100F0D` | Background (dark mode) |

**Theming:** CSS custom properties on `:root`, overridden via `@media (prefers-color-scheme: dark)` and `:root[data-theme]`. Light mode = paper background with ink text (matches the original brand sheet's own website mockup); dark mode = near-black background with paper text (matches the brand sheet's "reversed" logo lockup). Primary buttons use separate `--btn-bg`/`--btn-fg` tokens so they stay high-contrast in both themes.

| Font | Role |
|------|------|
| Space Grotesk | Wordmark, headings, nav, body |
| IBM Plex Mono | Tagline, eyebrows, mono labels |
| Instrument Serif | Editorial accents only (not currently used on the live page, reserved per brand sheet) |
| Tiro Devanagari Hindi | Hindi wordmark (सहयोग हब) in the About section |

Loaded via Google Fonts CDN — **this only works when hosted normally** (e.g. GitHub Pages); it will NOT load correctly if the file is ever published through a sandboxed environment with a strict CSP that blocks external font requests.

---

## Website Sections
1. **Header/Nav** — logo mark + wordmark, sticky, nav links (Work / Services / About) + "Get a quote" button (button stays visible on mobile even though nav links collapse)
2. **Hero** — headline "Websites, apps and ads that pay for themselves.", tagline eyebrow, two CTAs
3. **Services (01)** — three cards: Websites, Apps, Meta Ads
4. **Recent Work (02)** — case study: Meera Residency, Nimbahera, with a real screenshot of the live site (captured via html2canvas, not the Instagram poster mockup), stats (71 plots mapped / 2 languages / 50km ad radius), link to the live site
5. **Why Sahyog (03)** — brand meaning, approach, founder credit, Devanagari wordmark block
6. **Contact / Get a quote** — direct Call/WhatsApp/Email links + a form that opens WhatsApp with the visitor's details pre-filled via `wa.me` deep link (no backend, nothing stored)
7. **Footer** — logo, tagline, copyright

---

## Tech Stack
| Technology | Usage |
|------------|-------|
| **HTML5** | Single-file structure |
| **CSS3** | Custom properties for theming, Grid/Flexbox, light+dark mode, responsive breakpoint at 860px |
| **Vanilla JavaScript** | WhatsApp deep-link form submission only — no other JS logic |
| **Inline SVG** | Logo mark (pixel-exact port of the brand sheet's icon geometry, viewBox 0 0 150 100) |
| **Google Fonts CDN** | Space Grotesk, IBM Plex Mono, Instrument Serif, Tiro Devanagari Hindi |

**Files:**
- `index.html` — the site
- `assets/case-study-meera.png` — live screenshot of the Meera Residency site used as case-study proof

---

## Known Issues Fixed During Build
- A decorative low-opacity bracket background in the hero rendered as broken/misplaced boxes — removed rather than shipped half-working.
- Mobile header was hiding the entire nav including the "Get a quote" CTA — fixed so only text links collapse, button stays.
- Primary button had poor contrast in dark mode (dark ink button on near-black bg) — fixed with theme-aware `--btn-bg`/`--btn-fg` tokens.

---

## What Still Needs To Be Done
- [ ] **Hosting/domain** — deploy to a real domain or GitHub Pages (same pattern as the Meera Residency site)
- [ ] **More case studies** — currently only one (Meera Residency); add more as new client work is completed
- [ ] **Testimonials** — no client testimonials yet
- [ ] **Analytics** — no tracking installed
- [ ] **Favicon polish** — currently a small inline SVG data-URI favicon (32px, no center dot per brand rule); fine for now but a proper multi-size favicon set could be added later
- [ ] **Instrument Serif** — reserved in the brand system for "editorial accents" but not yet used anywhere on the live page

---

## Related Files
- Source website: `C:\Claude\Projects\sahyog-hub\SourceCode\index.html`
- Brand sheet (Claude Design project, still under its original name): `Sahyog Studio Premium Logo`, files `Sahyog Studio Brand Sheet.dc.html`, `Sahyog Studio Logo.dc.html`, `Sahyog Studio Logo - Tagline.dc.html`
- Related client project referenced as case study: `C:\Claude\Projects\meera-residency`
- Superseded folder (old name, kept until cleanup): `C:\Claude\Projects\sahyog-studio` — content is stale, use `sahyog-hub` instead
