# Online Graduate Diploma in Online Education

**Client:** AUB · **Faculty:** FAS (Faculty of Arts and Sciences)

Landing pages for this program. Assets in `assets/` are shared across all three.

| Page | File | Status | Indexing |
|---|---|---|---|
| Cold audience | `Cold_Audience_dc.html` | ✅ built | `index, follow` |
| In-market hero form | `In-Market_Hero_Form_dc.html` | not yet added | `index, follow` |
| Thank you | `Thank_You_dc.html` | not yet added | **`noindex, follow`** |

Cold and in-market pages must not share an FAQ set — duplicate `FAQPage` JSON-LD on
one domain splits search signals.

---

## Cold audience page

Long-form cold-audience LP, built from Think Orion's `Cold_Audience_dc.html` DC
template. Single self-contained file.

### What's in the file

- 7-question FAQ with matching `FAQPage` JSON-LD (visible text and schema are verbatim-identical).
- Two Vala form hosts: `#vala-funnel` (hero) and `#vala-funnel-2` (advisor section).
  Each sits below a static field mockup that must be replaced by the live embed.
- A standalone `<script>` before `</body>` replicates sticky-CTA / FAQ / CTA-scroll /
  slider behaviour for review outside the DC runtime. Remove once DC wiring is live.

### Head, indexing and tracking

Added to the `<helmet>` block (which is what DC injects into the production `<head>`):

| Tag | State |
|---|---|
| `robots` | `index, follow, max-image-preview:large` — this page carries its own FAQPage schema targeting cold-stage long-tail queries, so it is meant to be indexed. **The Thank You page must be `noindex, follow` instead.** |
| `canonical` | `[CANONICAL URL]` placeholder — needs the live URL |
| Favicon | Three `[FAVICON URL]` placeholders (ico, svg, apple-touch-icon) |
| Open Graph | Complete (`og:type`, `og:site_name`, `og:locale`, `og:title`, `og:description`, `og:url`, `og:image` + width/height/alt). `og:url` and `og:image` are placeholders. |
| Twitter card | `summary_large_image`, sharing the OG title/description/image |
| GTM | `window.dataLayer` initialised live. The loader snippet is **present but commented out** — a placeholder container ID would fire a 404 on every page view. Supply the real ID, uncomment, and add the matching `<noscript>` iframe as the first element in `<body>`. |

### Assets

Both photos are still embedded as base64 data URIs, so the file reviews standalone
with no external requests. They account for **~81KB — 52% of the file**; swapping
both `src` values to hosted URLs drops it from ~156KB to ~73KB.

The decoded originals are extracted and ready to upload to a CDN:

| File | Size | Used for |
|---|---|---|
| `assets/premise-educator-mce-badge-800x800.jpg` | 54KB | Premise section composite (includes the MCE badge) |
| `assets/advisor-mike-220x211.jpg` | 6KB | Advisor portrait |

Both `<img>` tags now carry `loading="lazy"`, `decoding="async"` and intrinsic
`width`/`height`. Neither is the LCP element — the hero is type and a form, no image —
so lazy-loading both is safe.

**Still needed from AUB** — four faculty portraits, currently `image-slot` placeholders that
render only inside the DC preview:

| Slot id | Portrait |
|---|---|
| `cold-fac-1` | Dr. Hoda Baytiyeh |
| `cold-fac-2` | Dr. Mahmud Shihab |
| `cold-fac-3` | Rayan Fayed |
| `cold-fac-4` | Rana Ghazzi |

Replace each `<image-slot>` with a plain `<img>` once the real photo exists — `image-slot`
elements are invisible in a raw browser.

### Open client-fill items

The full list lives in the comment block at the top of `Cold_Audience_dc.html`. Headlines:

- Intake shown as **Fall 2026**; the Aug 31, 2026 semester start comes from the AUB MA page
  (the diploma page still shows 2025). Confirm the diploma start date before launch.
- Faculty `[Short bio]` lines to be supplied.
- All testimonial quote blocks are `[TESTIMONIAL / NAME / ROLE]` placeholders with suggested angles.
- Comparison-table figures for the non-AUB columns are indicative ranges — client validates.
- Confirm the correct Vala funnel script for this program, and that the embed supports two mounts.
- Confirm Microsoft brand-usage approval for the MCE badge.
- Confirm the Lebanese MoE recognition wording (mirrors the client-reviewed email sequence)
  belongs on a paid landing page.
- Fill the `[CANONICAL URL]`, `[FAVICON URL]` and `[OG IMAGE URL]` placeholders; supply the
  GTM container ID and uncomment the loader.
- **Duplicate `viewport` meta is intentional for now.** One sits in the outer `<head>` beside
  `support.js` (the DC preview harness), one in `<helmet>` (the production head). Confirm with
  Manno which one actually ships before deleting either — removing the wrong one breaks the
  DC preview.

### QA status

Rendered in Chromium at 1440×900 and 390×844: no horizontal overflow at either width
(`scrollWidth == clientWidth`), tag balance clean, JSON-LD parses and all 7 Q&A pairs match
the visible copy verbatim. Both lazy images confirmed to decode at their full intrinsic size
(800×800 and 220×211) once scrolled into view, with no layout shift. Standalone behaviour verified — sticky CTA
hides over the hero and over `#form` and shows in between, FAQ accordions open/close with icon
rotation, CTAs scroll to `#form`, slider arrows show on mobile and hide on desktop.
