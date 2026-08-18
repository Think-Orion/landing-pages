# Think Orion — Landing Pages

HTML landing pages built for Think Orion clients.

Each page lives in its own folder, named for the client, faculty, program, and
page type, and ships as a single self-contained `_dc.html` file so it slots into
the DC pipeline. Per-page notes — outstanding client-fill items, assets still
needed, and QA status — live in that folder's `README.md`.

## Pages

| Client | Program | Page type |
|---|---|---|
| AUB — FAS | Online Graduate Diploma in Online Education | Cold audience |

## Conventions

- One folder per page. The deliverable keeps its template filename
  (`Cold_Audience_dc.html`, `In-Market_Hero_Form_dc.html`) so it slots into the
  DC pipeline unchanged.
- Real photos ship as plain `<img>` tags. `image-slot` elements are genuine
  placeholders — they render only inside the DC preview and are invisible in a
  raw browser.
- Client-supplied images may be embedded as data URIs for review builds; swap to
  hosted files at launch.
- Every page carries a client-fill comment block at the top of the HTML listing
  what still needs confirming before launch.
- Work happens on a branch and lands via pull request.
