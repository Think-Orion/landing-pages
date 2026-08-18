# Deployment checklist — Online Graduate Diploma in Online Education

Hand this to whoever deploys the page. Items marked **BLOCKING** will visibly break
something if skipped.

---

## 1. Files in this package

| File | Where it goes |
|---|---|
| `Cold_Audience_dc.html` | The page itself |
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

Two mount points are ready for the live Vala embed:

- `#vala-funnel` — hero form card
- `#vala-funnel-2` — advisor section form card

Confirm the embed supports **two mounts on one page**. The DC runtime mounts only
`#vala-funnel` by default.

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

---

## 7. Remove before launch

- The `<script>` immediately before `</body>` replicates sticky-CTA, FAQ, CTA-scroll and
  slider behaviour for review outside the DC runtime. Remove it once DC wiring is live.
- Four `<image-slot>` elements are faculty portrait placeholders. They render only in the
  DC preview and are **invisible in a normal browser**. Replace each with a plain `<img>`
  once real photos exist: Dr. Hoda Baytiyeh, Dr. Mahmud Shihab, Rayan Fayed, Rana Ghazzi.
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
  between. The footer carries `padding-bottom:104px` so the bar cannot cover the legal
  links at page bottom.
