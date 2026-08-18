# AUB — FAS — Online Graduate Diploma in Online Education — Cold Audience LP

Long-form cold-audience landing page, built from Think Orion's `Cold_Audience_dc.html`
DC template. Single self-contained file: `Cold_Audience_dc.html`.

## What's in the file

- 7-question FAQ with matching `FAQPage` JSON-LD (visible text and schema are verbatim-identical).
- Two Vala form hosts: `#vala-funnel` (hero) and `#vala-funnel-2` (advisor section).
  Each sits below a static field mockup that must be replaced by the live embed.
- A standalone `<script>` before `</body>` replicates sticky-CTA / FAQ / CTA-scroll /
  slider behaviour for review outside the DC runtime. Remove once DC wiring is live.

## Assets

Embedded as base64 data URIs (no external files needed to review this page):

- Premise image (the "You don't need a tech background" section composite, includes the MCE badge)
- Advisor portrait (Mike)

Swap both to hosted files at launch.

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

## Open client-fill items

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

## QA status

Rendered in Chromium at 1440×900 and 390×844: no horizontal overflow at either width
(`scrollWidth == clientWidth`), both embedded images load, tag balance clean, JSON-LD parses
and all 7 Q&A pairs match the visible copy verbatim. Standalone behaviour verified — sticky CTA
hides over the hero and over `#form` and shows in between, FAQ accordions open/close with icon
rotation, CTAs scroll to `#form`, slider arrows show on mobile and hide on desktop.
