# Deployment checklist — Online Graduate Diploma in Online Education

Hand this to whoever deploys the page. Items marked **BLOCKING** will visibly break
something if skipped.

---

## 1. Files in this package

Applies to **all three pages** unless noted.

| File | Where it goes |
|---|---|
| `Cold_Audience_dc.html` | Cold-audience page |
| `In-Market_Hero_Form_dc.html` | In-market page |
| `Thank_You_dc.html` | Post-submission page |
| `assets/Graduate_diploma_in_online_education_factsheet_2025.pdf` | Keep it reachable from the thank-you page — see §10 |
| `assets/favicon/*` | **Web root** of the serving domain — not next to the page |
| `assets/premise-educator-mce-badge-800x800.jpg` | Optional: host it and swap the data URI (see §5) |
| `assets/advisor-mike-220x211.jpg` | Optional: same |

---

## 2. Favicons — BLOCKING for the icon to appear

Every file in `assets/favicon/` must go to the **web root** of the domain serving the
page, because the page references them as root-relative paths (`/favicon.ico`):

```
/favicon.ico
/favicon-16x16.png
/favicon-32x32.png
/apple-touch-icon.png          ← use this one, it is flattened onto white
/android-chrome-192x192.png
/android-chrome-512x512.png
/site.webmanifest
```

Do **not** deploy `apple-touch-icon-source-transparent.png`. It is the original supplied
file, kept only for traceability. iOS ignores transparency on home-screen icons and
composites onto black, so the transparent version would ship as a seal on a black square.

If the page is served from a subdirectory rather than a domain root, tell us — the paths
need changing.

---

## 3. Canonical, og:url, og:image — BLOCKING before launch

**Landing pages only.** The thank-you page deliberately has no canonical and no Open Graph
tags — see §10.

Four tags are **commented out** in the `<head>` because the live URL was unknown at
handoff. Search for `REPLACE-WITH-LIVE-URL` in the HTML. Uncomment each and fill in:

| Tag | Value |
|---|---|
| `<link rel="canonical">` | This page's final absolute URL |
| `og:url` | Same value as canonical |
| `og:image` | Absolute URL to a hosted **1200×630** JPG or PNG |
| `twitter:image` | Same value as og:image |

Also uncomment `og:image:width`, `og:image:height` and `og:image:alt` alongside `og:image`.

**They were left commented rather than filled with placeholders on purpose.** A canonical
tag pointing at a placeholder can misdirect indexing, and a broken `og:image` makes every
social share render as a blank card. In both cases an absent tag is safer than a wrong
one, so nothing can ship broken by accident.

`og:image` must be an **absolute URL**. Relative paths and data URIs do not work — social
crawlers fetch it independently of the page.

---

## 4. Footer policy links — BLOCKING

Three footer links point at placeholders. Replace with AUB's **existing** policy pages:

- `[AUB PRIVACY POLICY URL]`
- `[AUB TERMS OF USE URL]`
- `[AUB NON-DISCRIMINATION / ACCESSIBILITY URL]`

These do not depend on where the page is hosted — they are absolute URLs on `aub.edu.lb`
that already exist, so they can be filled before handoff.

The privacy link matters beyond tidiness. The page collects name, email and phone, so a
privacy notice has to be reachable from the point of collection. Google Ads also requires
lead-gen destinations to disclose data practices, and a missing privacy link is a common
cause of ad disapproval.

---

## 5. The lead form — BLOCKING for the page to function

The page currently shows a **static mockup** of the lead form. It does not submit
anything: there is no `<form>` tag, the buttons are `type="button"`, and there is no
submit handler.

Mount points ready for the live Vala embed:

- **Cold page:** `#vala-funnel` (hero) and `#vala-funnel-2` (advisor section). Confirm the
  embed supports **two mounts on one page** — the DC runtime mounts only `#vala-funnel` by
  default.
- **In-market page:** `#vala-funnel` only.

When the form is wired, add the `dataLayer.push` for the conversion event — ask ops for
the expected event name and parameters. Nothing is tracked on submit today.

---

## 6. Tag Manager — already installed, do not modify

Stape server-side container **`GTM-KZDZDJJ`**, loaded first-party from `trk.aub.edu.lb`.
Supplied by AUB ops with "do not modify this code" and pasted verbatim.

Do not reformat, re-encode or pretty-print the obfuscated query parameter — it *is* the
container reference.

Two open questions for ops:

- **Consent Mode v2** — the default consent state normally has to be set on-page, above
  the GTM loader, or by a CMP. Not present yet. Confirm before running EEA traffic.
- **Conversion event** on form submit (see §5).

**Verify the thank-you page tag first.** A thank-you pageview is the usual conversion
signal, so if that one tag is wrong, conversions go uncounted while spend continues. Check
it in GTM preview mode before the campaigns go live.

---

## 7. Remove before launch

- The `<script>` immediately before `</body>` replicates sticky-CTA, FAQ, CTA-scroll and
  slider behaviour for review outside the DC runtime. Remove it once DC wiring is live.
- `<image-slot>` elements are placeholders. They render only in the DC preview and are
  **invisible in a normal browser**. Replace each with a plain `<img>` once real photos
  exist.
  - **Cold page:** 4 faculty portraits — Dr. Hoda Baytiyeh, Dr. Mahmud Shihab, Rayan Fayed,
    Rana Ghazzi.
  - **In-market page:** the same 4 portraits **plus the hero background photo**. Until it is
    supplied the hero shows only its dark gradient.
- All testimonial quotes are `[TESTIMONIAL / NAME / ROLE]` placeholders.
- Faculty `[Short bio]` lines are placeholders.

---

## 8. Content still to confirm with the client

- **Intake date.** Shown as Fall 2026. The Aug 31, 2026 semester start comes from the AUB
  MA page; the diploma page still showed 2025. Confirm before launch.
- **Comparison table** figures for the non-AUB columns are indicative ranges.
- **MCE badge** — confirm Microsoft brand-usage approval.
- **Lebanese MoE recognition wording** in the FAQ mirrors the client-reviewed email
  sequence. Confirm it belongs on a paid landing page.

---

## 9. Known behaviour that is not a bug

- **Favicons will not appear in a `raw.githack.com` or similar preview** served from a repo
  subfolder, because `/favicon.ico` resolves to the preview host's root. Verify on a real
  deployment.
- **Duplicate `viewport` meta.** One sits in the outer `<head>` beside `support.js` (the DC
  preview harness), one in `<helmet>` (the production head), so only one ships. Confirm
  with Manno which before deleting either — removing the wrong one breaks the DC preview.
- The sticky CTA bar is hidden over the hero and over the form section, and shown in
  between. The **cold** and **thank-you** pages carry `padding-bottom:104px` on the footer so
  the bar cannot cover the legal links at page bottom; the **in-market page** hides the bar at
  the footer instead and needs no padding. All three verified by hit test at 1440px and 390px.

---

## 10. Thank-you page specifics

- **`robots: noindex, follow`** — must never be indexed. It would rank for brand queries,
  expose the post-conversion state in search results, and inflate conversion counts with
  organic arrivals that never submitted the form.
- **No canonical, no Open Graph, by design.** Canonical is meaningless alongside `noindex`;
  Open Graph would invite social sharing of a page that should not be shared. Do not "fix"
  these by adding them.
- **Factsheet.** `assets/Graduate_diploma_in_online_education_factsheet_2025.pdf` is a
  compressed copy: **1.8MB, down from the 22.2MB original.** 77% of the original was one
  2551×14099px PNG reused as the background of all four pages, resampled to 150dpi. All four
  pages and all selectable text are intact and renders are visually indistinguishable. The
  22.2MB original is not in the repo — keep the client's copy as the source of truth. The
  download button uses a relative path and opens in a new tab; adjust the href if the PDF is
  hosted elsewhere.
- **Booking link** goes to Mike's Microsoft Bookings calendar in two places (Step 1 card and
  sticky bar). Confirm it is the right service for this program and that the meeting length
  there matches the "20 minutes" wording — Bookings pages are JS apps and cannot be read
  automatically.
- **Confirm the next-step promise.** The hero says a call within 48 hours. Verify with
  admissions that the first touch is a call, not an email, and that 48 hours is accurate.
- **Testimonials** are bracketed placeholders. Never publish them.
