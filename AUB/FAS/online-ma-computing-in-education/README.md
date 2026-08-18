# Online MA in Computing in Education

American University of Beirut · Faculty of Arts and Sciences · 100% online, asynchronous.

Three pages make up the funnel for this program. All three are self-contained
`_dc.html` files carrying the DC template filenames unchanged.

| Page | File | Status | Indexing |
|---|---|---|---|
| Cold audience | `Cold_Audience_dc.html` | ✅ built | `index, follow` |
| In-market hero form | `In-Market_Hero_Form_dc.html` | ✅ built | `index, follow` |
| Thank you | `Thank_You_dc.html` | ✅ built | **`noindex, follow`** |

The three page bodies were drafted against the client-approved Online Education
diploma builds and arrived complete. What this folder adds on top is the repo's
standing head/indexing/tracking block, the decoded image assets, the social share
image, and the QA pass recorded at the bottom of this file. One FAQ defect was
fixed during setup — see "FAQ de-duplication".

## Program facts used across the pages

| Fact | Value | Source |
|---|---|---|
| Credits | 30 (9 core courses × 3 credits + 3-credit capstone) | Derived — see "Credit maths" |
| Tuition | $450 / credit → $13,500 total | Approved diploma builds ($450/credit) |
| Duration | 1.5–2 years, ~7 weeks per course | Approved diploma builds (7 weeks/course) |
| Format | 100% online, asynchronous, no fixed class times | Factsheet prose, ×3 |
| Credential | AUB MA + Microsoft Certified Educator (MCE), MCE at no extra cost | Approved diploma builds |
| Recognition | NYSED-recognized; **not** accredited by the Lebanese MoE | Approved diploma builds |
| Admissions | Bachelor's (any field) from a recognized institution, min GPA 3.0, English proficiency, two recommendation letters | Factsheet + approved diploma builds |
| Diploma pathway | All 12 Graduate Diploma in Online Education credits transfer into this MA | Factsheet, footnote ** |
| Waivers | Students with an education or computer science background can apply to have credits waived | Factsheet, footnote * |
| Intake | Fall 2026 | Approved diploma builds |
| Advisor | Mike (Mike Wakim), Online Program Recruiter | Factsheet contact block |

### Credit maths

The factsheet's curriculum table lists **11 courses plus a capstone project** and
carries **no credit column and no tuition figure**. The pages present the degree as
**30 credits / 9 core courses + project**, treating `EDUC 300` (education) and
`CMPS 302` (computer science) as the two exemptible prerequisites named in the
factsheet's waiver footnote. 12 items × 3 credits = 36; less the two waivable
prerequisites = 30.

**This reconciliation is unconfirmed and it drives the headline price.** If a given
applicant does not have both prerequisites waived, the degree is 36 credits and
$16,200, not 30 credits and $13,500 — and the factsheet says the program is open to
graduates of *any* field, so the un-waived case is not the exception. Confirm the
default credit load with AUB before launch. See "Open client-fill items".

## Head, indexing and tracking

Applied to all three pages, matching the Online Education builds.

| Tag | State |
|---|---|
| `robots` | Cold and in-market: `index, follow, max-image-preview:large`. Thank you: **`noindex, follow`** — a post-submission page must never be indexed, and `follow` keeps link equity flowing to aub.edu.lb. |
| `canonical` | **Commented out.** The live URL is unknown at handoff, and a canonical pointing at a placeholder can misdirect indexing, whereas an absent one is safe — engines self-canonicalise. Uncomment and fill before launch. |
| Favicon | Root-relative paths (`/favicon.ico`, `/favicon-32x32.png`, `/favicon-16x16.png`, `/apple-touch-icon.png`, `/site.webmanifest`) plus `<meta name="theme-color" content="#8B1333">`. Files ship in `assets/favicon/` and must be deployed to the **domain root** — they will not appear in a raw-repo preview from a subfolder, which is expected. |
| Open Graph | `og:type`, `og:site_name`, `og:locale`, `og:title`, `og:description` live on both landing pages. `og:url`, `og:image` and its width/height/alt are **commented out** pending the live URL — a broken `og:image` renders a share as a blank card. The image file itself is supplied. The thank-you page carries no OG tags, matching the diploma build. |
| Twitter card | `summary_large_image`, title and description live; `twitter:image` commented out alongside `og:image`. |
| GTM | **Live.** Stape server-side container `GTM-KZDZDJJ`, loaded first-party from `trk.aub.edu.lb`. Pasted verbatim as supplied by AUB ops — the obfuscated query parameter *is* the container reference and must not be reformatted or re-encoded. |

`og:title` differs between the two landing pages on purpose ("Teach technology.
Design learning." vs "…Apply now.") so the two share cards are distinguishable.

## FAQ de-duplication

Both landing pages carry seven FAQs mirrored in `FAQPage` JSON-LD. As drafted,
**three questions were byte-identical across the two pages**, which splits search
signals when two pages on one domain answer the same query with the same schema.
The approved diploma build has zero overlap by design. The three in-market
questions were re-angled to the in-market frame:

| Was (collided with cold page) | Now |
|---|---|
| Is the AUB MA in Computing in Education recognized internationally? | How is the AUB MA recognized outside Lebanon? |
| Can I start with the Graduate Diploma before committing to the full MA? | Do I need the Graduate Diploma before applying to the MA? |
| Is the Microsoft Certified Educator (MCE) certification included in the AUB MA? | How do I earn the MCE certification during the MA? |

Two answer openings moved with their questions: the diploma answer now opens "No.
You can apply directly to the MA" (the question inverted, so a leading "Yes" would
have asserted the opposite), and the MCE answer drops its leading "Yes." because
"How do I earn…" is not a yes/no question. Visible copy and JSON-LD were changed
together and verified byte-identical. Overlap is now zero.

## Assets

Photos are embedded as data URIs for review builds; the decoded originals live in
`assets/` and the `src` values swap to hosted URLs at launch.

| File | Size | Used for |
|---|---|---|
| `assets/mce-classroom-robotics-1100x1100.jpg` | 155KB | Cold page premise section — educator and students with robotics kits, MCE badge composited top-right |
| `assets/advisor-mike-220x211.jpg` | 6KB | Cold page advisor portrait |
| `assets/factsheet-cover-300x400.jpg` | 33KB | Thank-you page factsheet thumbnail |
| `assets/og-image-1200x630.jpg` | 97KB | Social share card for both landing pages. Cropped from the classroom photo, framed to keep the MCE badge whole and the students' faces in view |
| `assets/favicon/` | 8 files | Root-deploy favicon set, copied from the Online Education build (same institution) |
| `assets/MA_in_Computing_in_Education_Factsheet_2025.pdf` | 2.8MB | Source factsheet, 2 pages |

### Image slots awaiting real photos

`image-slot` elements are genuine placeholders — they render only inside the DC
preview and are invisible in a raw browser. That is expected, not a bug.

| Slot id | Page | Needs |
|---|---|---|
| `hf-hero-bg` | In-market | Hero background photo |
| `cold-fac-1` / `hf-fac-1` | Both | Dr. Hoda Baytiyeh portrait |
| `cold-fac-2` / `hf-fac-2` | Both | Dr. Mahmud Shihab portrait |
| `cold-fac-3` / `hf-fac-3` | Both | Rayan Fayed portrait |
| `cold-fac-4` / `hf-fac-4` | Both | Rana Ghazzi portrait |

## Open client-fill items

Each page carries its own `CLIENT-FILL` comment block at the top. Consolidated:

1. **Credit load and total price** — the 30-credit / $13,500 headline assumes both
   prerequisites are waived. Confirm the default. This is the highest-impact open
   item on the build. See "Credit maths".
2. **Corporate group discount** — the cost FAQ on both pages states "corporate
   groups of five or more receive 15 to 20% off". This figure appears in no
   approved source and no client-reviewed material. Confirm or strike it.
3. **Weekly time commitment** — "10 to 15 hours per week" has no approved source;
   the diploma builds never quantified it.
4. **"Only online master's in the region"** — the cold hero's exclusivity claim.
   The factsheet supports "exclusive degree" and "interdisciplinary", not
   regional uniqueness. Confirm it is defensible or soften it.
5. **Live sessions vs asynchronous** — the factsheet's PROGRAM FORMAT strip reads
   "100% online courses | LIVE INTERACTIVE SESSIONS | ASYNCHRONOUS". The pages
   commit to fully asynchronous with no fixed class times, following the factsheet
   prose (which says asynchronous three times) and the approved diploma builds.
   Confirm there are no live obligations.
6. **Prerequisite mapping** — `EDUC 300` and `CMPS 302` named as the two
   exemptible prerequisites. The factsheet's waiver footnote names no courses.
7. **Testimonials** — the cold page's two graduate cards are `[BRACKETED]`
   placeholders with suggested angles. Never publish the placeholders.
8. **Faculty bios** — four named faculty, all bios `[BRACKETED]`. Instructor
   attribution in the cold curriculum cards covers `EDUC 371`–`374` only;
   instructors for the remaining courses and the capstone are outstanding.
9. **Intake** — "Fall 2026" mirrors the approved builds. Confirm the date.
10. **Factsheet download** — the thank-you page's download button is `href="#"`
    pending a hosted URL for the PDF in `assets/`.
11. **Booking link** — the thank-you page points at the Online Education
    Bookings calendar. Confirm the correct calendar for this program and that the
    meeting length matches the "20-minute" wording.
12. **Vala form embeds** — the DC runtime mounts `#vala-funnel`. The cold page has
    two form locations (hero + advisor section); confirm whether the embed
    supports a second instance or whether the advisor form should point at the
    hero.
13. **MoE caveat** — wording mirrors the client-reviewed email sequence. Confirm
    it should appear on paid landing pages.

## QA status

Chromium (Playwright), file:// loads, standalone behaviour script active.

| Check | Result |
|---|---|
| Render 1440×900 | Pass — `scrollWidth == clientWidth` on all three pages |
| Render 390×844 | Pass — `scrollWidth == clientWidth` on all three pages |
| Console / page errors | None, excluding the expected missing `support.js` and `image-slot.js` in a raw file:// load |
| HTML tag balance | Balanced on all three pages |
| FAQ JSON-LD ↔ visible copy | 7/7 questions and 7/7 answers match byte-for-byte on both landing pages |
| Cold ↔ in-market FAQ overlap | Zero |
| FAQ accordions | Expand and collapse, icon rotates, on both pages |
| Curriculum accordions | 10 per page, expand on click |
| Sticky CTA | Hidden over the hero, visible mid-page, hides again at the form — both pages |
| Nav CTA | Brings the form into view on both pages (on the in-market page the form is in the hero, so the scroll goes up — correct) |
| Testimonial slider | Fits at 1440 with arrows hidden; overflows and scrolls at 390 |
| Thank-you page | Two booking links resolve; one `href="#"` placeholder remains, the factsheet download |

Page heights: cold 8350px desktop / 13053px mobile; in-market 5020 / 7626;
thank you 2085 / 2388.
