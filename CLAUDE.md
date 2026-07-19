# GK1 Energy Site

Static marketing site for Bill Geyer / GK1 Energy — an independent energy advisor
(solar, battery storage, heat pumps, generators). Two hand-coded HTML pages, no
build step, no framework.

## Pages

- `index.html` — residential site, lives at the site root (`gk1.energy/`).
  Has the lead-gen contact form (`#leadForm`) and the state-by-state incentive
  tiles (CT/MA/NH/ME — currently stub content pending real copy).
- `commercial-solar.html` — commercial & nonprofit site
  (`gk1.energy/commercial-solar.html`). Its own "Get in touch" CTAs route back
  to `index.html`'s shared contact form via `?interest=commercial#contact`,
  which `index.html` reads via JS to prefill the interest field.

Naming convention: keep `index.html` at the root (best for SEO/bookmarks — a
deliberate choice, not an oversight). New sub-pages should use plain,
description-based slugs (e.g. `commercial-solar.html`), not
`bill-geyer-*`-style filenames — cleaner URLs were an explicit ask.

## Hosting & deployment (Spaceship / cPanel)

- Host: Spaceship, cPanel account `adomzbmfbe`.
- **Real document root for gk1.energy is the `gk1.energy` folder**
  (`/home/adomzbmfbe/gk1.energy/`) — confirmed by live-testing an upload.
- `public_html` in the same account is an unrelated/unused folder, not
  gk1.energy's doc root. Don't assume it needs updating.
- **Sitejet Builder is a dead end** — it appears in cPanel's Domains tools but
  has no actual published site for gk1.energy (clicking into it offers to
  create a new site from scratch). It is not what serves the live domain.
  Don't waste time investigating it again.
- LiteSpeed Cache (`lscache`) is active on the account — after uploading
  changed files, a cache purge (or a short wait) may be needed before the
  live site reflects the change.
- **Deploys are currently manual**: edit locally → commit to git → when Bill
  says a change is ready to go live, upload the changed file(s) via cPanel
  File Manager into the `gk1.energy` folder, overwriting as needed.
- No CI/CD yet. A GitHub Actions + FTP/SFTP auto-deploy-on-push pipeline was
  discussed and deliberately deferred — Bill wants to keep making local edits
  and commits without them going live automatically while he's still
  reworking content. Revisit this when he says he's ready.
- git remote is `https://github.com/billgeyer/gk1-energy-site.git`. Pushing
  to GitHub only updates the repo, it does **not** touch the live site.

## Contact info

- Footer phone number: `(978) 358-1296` (Google Voice number for GK1),
  wired as a `tel:+19783581296` link in both page footers.
- Email: `bill@gk1.energy`.

## Current known gaps / in-progress

- CT/MA/NH/ME incentive tiles in `index.html` are still stub/placeholder
  copy — real state-specific content and source links are pending.
- Bill is planning a round of content rewrites across both pages; don't push
  anything live without confirming first.
