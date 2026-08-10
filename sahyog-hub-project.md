# Sahyog Hub — Project Knowledge Base

## Project Overview
The marketing/portfolio website for **Sahyog Hub**, a small digital agency founded by **Vimal** offering websites, apps, and Instagram/Facebook ad campaigns to local businesses. Single self-contained HTML file + SVG assets — no frameworks, no build tools.

> **Naming history:** the brand was originally **Sahyog Studio**, later renamed to **Sahyog Hub**. All site copy and file/folder names were updated at that time.

---

## REDESIGN — "ORANGE" (2026-08-07)

The site was rebuilt on an entirely new design, replacing the previous single-scrolling-page bronze/ink build. Source: claude.ai/design project `aacceed7-8584-4492-8c98-b76ed872b64c`, file `Sahyog Hub Website.dc.html` plus its embedded design system `_ds/sahyog-design-system-500147ca-...`, imported via DesignSync and reimplemented in plain HTML/CSS/vanilla JS per StaticSiteTemplate.md's design-import guidance (no DC-runtime, no `support.js`, no `image-slot.js` shipped).

### What the redesign CHANGED
| | Before | After |
|---|---|---|
| Brand colour | Bronze `#B4763C` on ink `#2C3040` | **Orange `#ea6018`** on white, with peach `#fff0e8` bands |
| Fonts | Space Grotesk + IBM Plex Mono | **Poppins** (display) + **DM Sans** (text) |
| Logo | Two-bracket mark `[ · ]` | **Wordmark only** — "Sah**yog** Hub" with "yog" in orange. No icon mark in the design. |
| Structure | One scrolling page, anchor links | **Four pages** — Home / Services / Work / Contact *(superseded 2026-08-10 — see Site Structure; it is a single scrolling page again)* |
| Dark mode | Full light + dark theming | **Light only** — the design ships no dark palette |

**This is a real brand shift, not just a reskin.** The bronze/ink brand sheet (`Sahyog Studio Premium Logo` design project) and the artefacts in `Docs/` (`logo-directions.png`, `logo-s-ribbon.png`, `illustrations.png`) are all now **out of date** relative to the live site. Either refresh them to orange or treat them as historical.

### What was KEPT from the old site
- Real contact details: +91 95668 12835 (call + WhatsApp), vimaljkasp@gmail.com
- The WhatsApp-deep-link quote form (no backend, nothing stored)
- All three case studies and their real live-site screenshots
- The सहयोग / "Together, we build" line *(the "Founded by Vimal" credit was removed on the owner's request, 2026-08-07 — do not reinstate it from a design import)*
- Live links to all three client sites

---

## Brand Identity (current)
| Field | Value |
|-------|-------|
| Name | Sahyog Hub (सहयोग हब) |
| Meaning | Sahyog (सहयोग) = collaboration/cooperation |
| Tagline | "Together, we build" |
| Services line | Websites · Apps · Marketing Ads |
| Founder | Vimal |
| Location | Rajasthan, India |

---

## Contact Details
| Channel | Value |
|---------|-------|
| Call | +91 95668 12835 |
| WhatsApp | +91 95668 12835 (`wa.me/919566812835`) |
| Email | vimaljkasp@gmail.com |

---

## Design System (from the design project's tokens, copied verbatim)
**Orange ramp:** 50 `#fff5ef` · 100 `#ffe6d7` · 200 `#ffd0b5` · 300 `#fbb089` · 400 `#f5854f` · **500 `#ea6018` (brand)** · 600 `#d55311` (hover) · 700 `#b1420b` (press) · 800 `#8a3308` · 900 `#5e2205`

**Neutrals:** ink 900 `#1e1e1e` (headings) · 600 `#6b6b6b` (body) · 500 `#8a8a8a` (muted) · 300/200/100 · white

**Service tile accents:** yellow `#f5c400` (Websites) · green `#22c55e` (Apps) · violet `#7c5cf0` (Marketing Ads)

**Surfaces:** page `#ffffff` · warm band `#fff0e8` · card border `#f1e7e0`

**Type:** Poppins 400/500/600/700 (display) · DM Sans 400/500/700 (text). Display 56 / h1 44 / h2 34 / h3 24 / h4 18 / body-lg 17 / body 15 / body-sm 14 / caption 12.5 / micro 11.

**Layout:** container 1140px, gutter 24px, section padding 96px (64px small), header breakpoint **860px**.

Fonts load from Google Fonts CDN — fine on normal hosting, would fail under a strict CSP.

---

## Site Structure — single scrolling page

**Changed 2026-08-10 ("Kinetic").** The four hash-routed pages are gone. Everything is now one scrolling page with anchor navigation, per the `Sahyog Hub Kinetic.dc.html` design.

Anchors: `#services` · `#work` · `#process` · `#contact` (plus `#top`). Plain native anchor links — no router, and no JS is required to navigate. `html{scroll-behavior:smooth}` is the only enhancement, and it degrades to an instant jump.

**Header** — not sticky (the design does not make it so; it scrolls away).
**Hero** — eyebrow, a two-line headline where each line rises out of an `overflow:hidden` clip, lead paragraph + two CTAs side by side, then **three illustrations in a row** that pop in and then idle-float on staggered loops.
**Ticker** — full-bleed orange marquee, duplicated track scrolling `translateX(-50%)` over 30s.
**Services** — three cards, each now with a **three-point bullet list** under the description. Note the middle card is "Applications", not "Apps", in this design.
**Work** — three client cards on the peach band.
**Process** — a horizontal rule that draws itself in (`scaleX(0)` → `scaleX(1)`), then four numbered steps.
**Contact** — heading, call/WhatsApp/email cards, floating armchair illustration, quote form.
**Footer** — wordmark + tagline, Services / Work / Contact columns, orange copyright bar.

There is no CTA banner in this design, and no separate Services/Work pages.

> **Work cards keep the proof detail added on 2026-08-07** — category eyebrow, green "Live" dot, feature pills, and the **live domain spelled out** instead of a generic "View live site". The Kinetic design specifies the plainer version; this was kept deliberately because it was an explicit owner request and is purely additive.

> **The footer tagline in the design reads "…founded by Vimal".** That was dropped — the owner asked on 2026-08-07 for their name to come off the site. Do not reinstate it when re-importing a design.

---

## Motion

Keyframes are all prefixed `k-`: `k-rise` (headline lines), `k-in` (fades), `k-float` (idle bob), `k-ticker` (marquee), `k-pop` (hero illustration entrance).

**Reveals use CSS transitions, not keyframes, and are driven by IntersectionObserver.** Two reasons, both found the hard way:

1. The design puts fixed `animation-delay` values on every section, and they all start on page load. Anything below the fold therefore finishes animating before it is ever scrolled into view, so the visitor sees nothing happen. Observing intersection is what "kinetic" is actually reaching for.
2. With keyframes plus `both` fill, the `prefers-reduced-motion` override (`*{animation:none}`) would strand elements on their `opacity:0` first frame — a blank page for anyone with that setting enabled. Transitions degrade to "just visible" instead.

**Three guards stop content ever being stranded invisible.** This matters because the reveal pattern hides content by default and relies on JS to show it:

- The hidden start state is scoped behind a `.js` class set **synchronously in `<head>`**. No JS — blocked, failed, ancient browser — means nothing is ever hidden in the first place.
- `prefers-reduced-motion` reveals everything immediately with no transitions.
- A **1500 ms `setTimeout` safety net**: if no `.rv` element has revealed by then, force them all visible via a `.now` class that also kills the transition. `IntersectionObserver` and `requestAnimationFrame` do **not** run while a page is not being composited (background tab, some embedded viewers); timers still do. Without this the page can render blank — which was observed in practice during this build, not theorised.

---

## Tech Stack
| Technology | Usage |
|------------|-------|
| **HTML5** | Single file, one scrolling document with anchor sections |
| **CSS3** | Design tokens as custom properties, Grid/Flexbox, `auto-fit minmax` responsive columns, one media query at 860px for the nav, one for the iOS input-zoom fix |
| **Vanilla JS** | Mobile drawer, IntersectionObserver reveals + safety net, quote-form validation and WhatsApp deep link. ~80 lines, no dependencies. |
| **Inline SVG** | All icons (hand-written equivalents of the design's Lucide glyphs — the design masks them from a `unpkg` CDN, which would have added a runtime dependency) |
| **Google Fonts CDN** | Poppins, DM Sans |

**Files:**
- `index.html` — the whole site
- `assets/ill-*.webp` ×5 — what browsers actually download (179 KB total)
- `assets/ill-*.png` ×5 — the design's original 3D illustrations, RGBA; fallback only (see below)

> `ill-desktop-code.*` is **currently unreferenced** — the Kinetic design uses only four illustrations (whiteboard, desk-charts, bean-mail in the hero; armchair-tablet in contact). Both its PNG and WebP are kept rather than deleted: they cost no bandwidth (nothing requests them) and the design has changed twice in a week.
- `assets/og-image.jpg` — 1200×630 social preview card
- `assets/case-study-meera.png`, `case-study-leela.jpg`, `case-study-mewad.jpg` — real live-site screenshots

> **Screenshots go stale when a client site is redesigned.** `case-study-mewad.jpg` was re-captured on 2026-08-07 because Mewad Gir Farms had been rebuilt on its "Olive" design — the old capture showed the retired dark theme with a blank box where the hero video sat. Meera and Shree Leela were checked at the same time and still match (verified by page background: `#0c1520` navy and `#2a1512` maroon respectively). **Re-check all three whenever a client site is redesigned.** Capture with html2canvas at an explicit width/height — on some of these sites `window.innerWidth/innerHeight` read 0, which silently produces a 0×0 canvas.

---

## Illustrations — the real artwork, and how it got here

The five illustrations are the design project's own 3D-rendered PNGs, supplied manually by the owner.

They could **not** be fetched through DesignSync: `get_file` caps reads at 256 KiB and every one of these exceeds it, so each came back at exactly 196,608 decoded bytes with `"truncated": true` and **no IEND chunk** — a corrupt PNG that would still partially decode. (Same failure mode StaticSiteTemplate.md warns about, and the same one hit on Mewad Gir Farms.) The site briefly shipped hand-drawn flat-vector SVG stand-ins; those were deleted once the real files arrived. **If these ever need re-fetching, download them through the browser — do not trust a DesignSync read of them.**

| File | Intrinsic size | Displayed at | Used on |
|---|---|---|---|
| `ill-desk-charts.png` | 658×802 | 470px | Home hero |
| `ill-whiteboard.png` | 668×748 | 400px | Home process |
| `ill-desktop-code.png` | 768×772 | 430px | Services — Websites |
| `ill-armchair-tablet.png` | 694×758 | 430px / 300px | Services — Apps; Contact |
| `ill-bean-mail.png` | 658×702 | 430px | Services — Marketing Ads |

All five are **RGBA with real transparency** — they sit directly on the white and peach `#fff0e8` bands. Do **not** convert them to JPEG; that would drop the alpha and put a white box on the peach sections.

**Served as WebP — the PNGs are fallback only.** The source PNGs total 2.3 MB, which was far too heavy for customers on mobile data. Each is now also shipped as WebP and delivered via `<picture>`:

```html
<picture style="display:block;width:100%;max-width:470px;margin-left:auto">
  <source srcset="assets/ill-desk-charts.webp" type="image/webp">
  <img src="assets/ill-desk-charts.png" width="658" height="802" …>
</picture>
```

| | PNG | WebP |
|---|---|---|
| Five illustrations | 2,310 KB | **179 KB** (−92%) |
| Hero alone (LCP) | 487 KB | **40 KB** |

Any browser without WebP support silently gets the PNG; Chrome never requests it (verified — `currentSrc` is `.webp` for all five).

> **How the WebP files were made:** no `sharp`, `cwebp` or ImageMagick is available in this environment (and note `convert` on Windows' PATH is the filesystem utility, *not* ImageMagick). They were encoded with **Chrome's own canvas encoder** — `fetch` the PNG same-origin → `createImageBitmap` → `canvas.toDataURL('image/webp', 0.86)` → decode the base64 to disk. Same trick works for re-encoding later. Verified afterwards that every file has a `RIFF/WEBP/VP8X` header **with the alpha flag set** — alpha matters, these sit on the peach bands and a flattened version would show a white box.

**Sizing lives on the `<picture>`, not the `<img>`.** `<picture>` is inline by default and shrinks to fit, so `margin-left:auto` / `margin:0 auto` on the inner `<img>` would silently stop positioning anything. The wrapper carries `display:block;width:100%;max-width:…` and the img is just `width:100%;height:auto;display:block`.

**Loading strategy.** All four pages live in the DOM at once, so a naive build would pull every illustration on first paint. Instead:
- The hero (`ill-desk-charts`) is eager with `fetchpriority="high"` — it is the LCP element.
- Every other illustration carries `loading="lazy" decoding="async"`. Because the Services and Contact pages are `display:none` until routed to, their images are never fetched until the visitor actually opens those pages.
- Verified: Home first paint requests **2** illustrations, not 5; the other three arrive only on navigating to Services.

Each `<img>` also carries its true intrinsic `width`/`height` so the aspect ratio is reserved and there is no layout shift while they load.

> The real PNGs are **portrait** where the temporary SVGs were landscape, so the hero is taller than it was — 733px. On a 720px-tall viewport that pushes the next section just past the fold; at the design's own target height (1280×900) it sits comfortably. Not a bug, but worth knowing if the hero is ever re-tuned.

---

## Deliberately NOT Implemented

**Testimonials.** The design has a "What Clients Say!" section with two cards reading `[Client name]`, `[Role, company]` and `[Placeholder — a sentence on what the site changed for their business.]`, and its own subtitle says *"replace these with real client words before the site goes live."* Shipping it would have meant either publishing literal `[Client name]` placeholders or **inventing client quotes**, which would be fabricated social proof on a live commercial site. The section is omitted entirely. Add it back once real, attributable quotes exist — the card styling is straightforward (avatar initial in an orange circle, name in orange, role in muted micro text, quote, star rating).

---

## Bugs Found and Fixed During This Build
| Issue | Cause | Fix |
|---|---|---|
| Wordmark rendered as "SahyogHub" | `.wordmark` was `display:flex`; a flex container discards the whitespace text node between the `<span>` and "Hub" | Made it `display:inline-block` with `line-height:44px` (keeps the 44px touch target without flex) |
| Service deep-links (`#/services#svc-apps`) switched page but never scrolled | Only used `window.scrollTo({behavior:"smooth"})`, which is deferred indefinitely in embedded/preview contexts — the original design's author had already hit this and shipped a fallback, which was lost in reimplementation | Restored the fallback: after 380ms, if `pageYOffset` is still >4px from target, set `scrollingElement.scrollTop` directly |
| Top ~13px of all three service icon tiles was clipped off | One `.card-flush` class carrying `overflow:hidden` was applied to both the service and work cards. Work cards *must* clip (so the screenshot corners follow the card radius) but service cards must not — their icon tile is positioned at `top:-14px` to overhang the card edge. The design used two separate prop sets (`cardFillProps` vs `cardClipProps`) for exactly this reason. | Split into `.card-flush` (no clip, service cards) and `.card-clip` (clips, work cards) |
| iOS Safari zoomed the viewport whenever a quote-form field was focused, leaving visitors pinched in | All five controls inherited `--fs-body` (15px). iOS force-zooms any focused control under 16px. | `@media(max-width:859px){.field input,.field select,.field textarea{font-size:16px}}`. **This rule must stay *after* the `.field` block** — it has identical specificity, so source order is what makes it win. Desktop stays 15px as designed. |
| *(Kinetic)* Whole page could render **blank** | The reveal pattern hides content by default and reveals it with JS. `IntersectionObserver` and `requestAnimationFrame` do not run while a page is not being composited, so nothing ever revealed. Observed live, not hypothetical. | Three layers: a `.js` class set synchronously in `<head>` so the hidden state only applies when JS runs at all; immediate reveal under `prefers-reduced-motion`; and a 1500 ms `setTimeout` net that force-reveals with transitions disabled. See **Motion**. |
| *(Kinetic)* Scrolling and sticky positioning broken | `overflow-x:hidden` on `body`. Per spec, setting one axis to non-`visible` forces the other to compute to `auto` — measured: `body` `overflow-y` became `auto` with `clientHeight` 6878px, i.e. body became a scroll container the full height of the document. | Removed it. The hero and ticker already clip themselves, and a 320px audit confirms nothing else overflows, so no page-level clip is needed. Verified `body` `overflow-y` is back to `visible`. |

---

## Mobile Audit + Testing (2026-08-10, "Kinetic" build)

Swept **320×720, 375×812 and 414×896**, plus desktop 1280. Zero console errors throughout.

- **Horizontal overflow: none** at any width — `document.scrollWidth` equals the viewport exactly. The only elements wider than the viewport are inside `.ticker-track`, which is deliberately over-wide and clipped by `.ticker{overflow:hidden}`.
- **Tap targets:** nothing under 40px except the header's `btn-sm` "Get A Quote" at 34px — that is the design's own `--control-h-sm`, it only renders at ≥860px where the pointer is a mouse, and the mobile drawer's equivalent is a 50px `btn-lg`. Not a touch-target defect.
- **Section flow:** services → work → process → contact tile contiguously with zero gaps (987/1588/2429/2937 at 1280px).
- **Form:** empty submit blocked with both field errors; a 5-digit phone still blocked; valid submit produces the correct `https://wa.me/919566812835?text=…` with a well-formed message.
- **Links:** all `tel:`/`wa.me`/`mailto:` point at the real number and address; all three external client links carry `rel="noopener"`; the owner's name appears nowhere in the copy.
- **Drawer:** opens, sets `aria-expanded`, and closes when a link inside it is used.
- **Images:** all three hero illustrations serve `.webp`; the contact illustration stays deferred until scrolled to; no broken images.
- **Fields:** 16px on mobile (iOS zoom fix holds), 15px on desktop.

### Not verifiable in this environment
The preview pane was **not compositing** during this build, which means `IntersectionObserver`, `requestAnimationFrame`, CSS transitions and **scrolling itself** were all inert — assigning `scrollingElement.scrollTop` returned 0. So the following were reasoned about and guarded, but **not** observed working end to end:

- the staggered reveal animations actually playing,
- anchor-link scrolling landing on each section.

Both are ordinary browser behaviour and the fallbacks are in place, but they are worth a quick manual check on the live site.

> **Two testing gotchas worth remembering.** (1) `npx serve` plus browser caching will serve a stale `index.html` and make a correct fix look broken — reload with `location.replace('/?v='+Date.now())` before doubting the CSS. (2) `html2canvas` cannot rasterise externally-referenced images, so page captures show blank illustration slots; that is a capture artefact, not a site bug.

---

## What Still Needs To Be Done
- [x] **Hosting/domain** — LIVE at sahyoghub.com / www.sahyoghub.com via Cloudflare Pages, repo https://github.com/vimaljkasp/sahyog-hub
- [x] **Analytics** — Cloudflare Web Analytics, zone-wide, zero code changes
- [x] **Real illustrations** — the design's five PNGs are in, lazy-loaded (see above)
- [x] **Image weight** — WebP via `<picture>`, 2,310 KB → 179 KB (−92%); hero 487 KB → 40 KB
- [x] **og:image** — 1200×630 card at `assets/og-image.jpg`, wired up with Open Graph + Twitter tags
- [x] **Bronze-era artefacts** — moved to `Docs/archive-bronze/` with a README explaining what they were and why they no longer apply
- [ ] **Testimonials** — still blocked on real client quotes. See above; inventing them is not an option.
- [ ] **Logo mark** — the new design is wordmark-only; decide whether the bracket mark is retired for good or gets an orange version for the favicon and social avatar
- [ ] **Favicon** — currently an orange tile with a white "S" as an inline data-URI; a proper multi-size set (and a real social avatar) would be better
- [ ] **More case studies** — three so far

---

## Related Files
- Source website: `C:\Claude\Projects\sahyog-hub\SourceCode\index.html`
- Current design project: `aacceed7-8584-4492-8c98-b76ed872b64c` — **`Sahyog Hub Kinetic.dc.html` is the one the live site is built on** (2026-08-10). `Sahyog Hub Website.dc.html` in the same project is the superseded four-page version; `Sahyog Hub Logo.dc.html` is the wordmark.
- Superseded bronze brand sheet: design project `5f9ff2f5-ed87-4349-8081-0fa0f468f410` (`Sahyog Studio Premium Logo`)
- Client projects used as case studies: `C:\Claude\Projects\meera-residency`, `C:\Claude\Projects\shree-leela-restaurant`, `C:\Claude\Projects\mewad-gir-farms`
- Shared static-site conventions: `C:\Claude\Projects\StaticSiteTemplate.md`
