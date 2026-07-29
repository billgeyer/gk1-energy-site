# GK1 Energy Site

Static marketing site for Bill Geyer / GK1 Energy — an independent energy advisor
(solar, battery storage, heat pumps). Three hand-coded HTML pages
(`index.html`, `business-solar.html`, `privacy-policy.html`), no build step,
no framework. Generators were deliberately dropped as a residential
offering — see `docs/decisions.md`; don't reintroduce the term without a
deliberate positioning decision.

Mental model: the site is designed as an extension of Bill's business card —
most visitors will already know who he is before they land here. It's not
optimized for cold organic search traffic.

Full rationale/decision history (why sections were merged, sourcing trails for
every state incentive figure, the OG-image gotcha, etc.) lives in
`docs/decisions.md` — read that on demand when a task needs the *why*, not
every session. This file is the always-loaded current-state summary.

## Pages

- `index.html` — residential site, root (`gk1.energy/`). Sections top to
  bottom: hero → How This Works (+ Recheck trust strip) → Rate News →
  What I Offer (Solar / Battery Backup / Heating & Cooling tiles) → The
  Process (4 steps, converted to the same details/summary tile pattern as
  the rest of the site 2026-07-28, was a static 4-column grid before) →
  Background & Credentials (3 tiles: Inverter & Battery Manufacturer Rep,
  Utility-Scale & Community Solar, Recheck verification) → Financing
  (4 methods + state-by-state incentives, CT/MA/NH/ME) → Get in touch
  (`#leadForm`). 7 `<section>` blocks plus the hero header.
- `business-solar.html` — Business Solar site for local business owners.
  Primarily owner-occupied buildings, but as of 2026-07-29 the "Who This Is
  For" copy also acknowledges landlords with commercial tenants as
  potentially viable, depending on lease structure, not a hard exclusion
  anymore. Sections: hero (headshot + hero-grid layout added 2026-07-29,
  matches index.html's pattern exactly, same CSS copied verbatim) → How
  This Works (incl. a paragraph on why commercial engineering/financing/tax treatment differs
  from residential, not just "bigger") → Who This Is For (3-question
  owner-occupied/roof/bill test) → System Types (System Types / Battery
  Storage tiles) → What It Actually Delivers (Cost Savings / Sustainability
  & ESG / Tax Incentives tiles, pure benefits, no product tiles mixed in) →
  The Process (5 tiles, same details/summary pattern as index.html:
  Discovery / Proposal / Letter of Intent and Deposit / Site survey &
  engineering / Installation & turn-on — LOI step added 2026-07-29) → Get
  in touch. CTAs route to `index.html`'s shared contact form via
  `?interest=commercial#contact`. System Types and What It Delivers used to
  be one combined section; split 2026-07-29 because mixing product tiles
  (System Types, Battery Storage) with benefit tiles (Cost Savings, ESG,
  Tax Incentives) under one heading read as incoherent.
- Almost every major section on both pages ends with a short contextual
  "Let's talk it through →" line linking to the contact form. When adding a
  new section, add one of these too, phrased for that section's topic. Use
  `&nbsp;→` (not a plain space) before the arrow so it can't wrap onto its
  own line.
- `images/` — headshot (hero photo on both pages as of 2026-07-29;
  previously index.html only), `gk1-icon-transparent.svg` /
  `gk1-icon-navy-bg.svg` (business-card logo mark, favicon + nav icon on
  both pages), `gk1-og-image.png` (OG/Twitter share image — see
  `docs/decisions.md` before regenerating). Keep images compressed
  (<500KB) before adding.
- When a positioning/scope change lands (e.g. the landlord-inclusion
  change above), check the `<meta property="og:description">` /
  `<meta name="twitter:description">` tags too — they're easy to miss
  since they're invisible in normal browsing, only surface in social
  previews and search results, and drifted stale once already
  (business-solar.html said "owner-occupied buildings" for a day after
  the copy itself had already broadened to include landlords).
- `privacy-policy.html` — linked from both footers. Matches actual current
  practice (Zoho CRM + Cal.com as the only data processors, no analytics/SMS
  automation claimed). **Keep accurate as practices change.**

Naming convention: `index.html` stays at the root (deliberate, for
SEO/bookmarks). New sub-pages use plain description-based slugs (e.g.
`business-solar.html`), not `bill-geyer-*`-style filenames.

## Active conventions

- Positioning: independent advisor, not installer — "my installation
  partner handles..." not "I handle...". Never imply Bill designs/installs.
- Financing copy stays general/educational — never cite a specific lender's
  rates/FICO minimums as Bill's own offer.
- Battery framing intentionally differs between pages (residential =
  "Battery Backup"/resilience, business = "Battery Storage"/peak shaving) —
  not an inconsistency, don't unify it.
- "Heating & Cooling" is the section label, "heat pump(s)" is the product
  term — never "mini-split" or "HVAC" in visible copy (HVAC is fine in
  Zoho-generated JS text and code comments).
- "Commercial" is reserved for citing actual legal/tax-code terms — GK1's
  own copy always says "business solar," never "commercial solar."
- **No em dashes in visible reader-facing copy, site-wide** (Bill's
  explicit call). Internal code comments are exempt. Title tags/footer
  separators use `·`.
- Do not pull content from the "Helio Solar Finance Training Guide" PDF
  into the public site — see `docs/decisions.md` for why.

## Hosting & deployment (Spaceship / cPanel)

- Host: Spaceship, cPanel account `adomzbmfbe`.
- **Real document root for gk1.energy is the `gk1.energy` folder**
  (`/home/adomzbmfbe/gk1.energy/`), not `public_html` (unrelated/unused).
- Sitejet Builder in cPanel is a dead end — not what serves the live domain.
- LiteSpeed Cache (`lscache`) is active — a purge or short wait may be
  needed after uploading before the live site reflects a change.
- **Deploys are manual**: edit locally → commit → when Bill says a change
  is ready, upload the changed file(s) via cPanel File Manager into the
  `gk1.energy` folder. No CI/CD yet (deliberately deferred while Bill is
  still reworking content).
- git remote: `https://github.com/billgeyer/gk1-energy-site.git`. Pushing
  to GitHub does **not** touch the live site.
- **Commit and push after essentially every change** — Bill's only copy of
  this work lives on one laptop, git push is the off-machine backup.
- **IMPORTANT — live site is stale.** As of the last session, gk1.energy
  only has the very first round of manual uploads. Everything since
  (Recheck section, Process sections, headshot, Financing, contextual
  CTAs) exists only in git/GitHub, not live. Don't assume gk1.energy
  reflects the current repo state — check with Bill before referencing
  "what's live."

## Contact info

- Footer phone: `(978) 358-1296` (Google Voice), `tel:+19783581296`.
- Email: `bill@gk1.energy`.

## Lead capture & scheduling architecture

- **CRM**: Zoho CRM, direct **Web-to-Lead** integration (n8n deliberately
  rejected as overkill for current volume). `#leadForm` in `index.html`
  POSTs directly to Zoho. Field details/history: `docs/decisions.md`.
- **Cal.com — implemented**: `https://cal.com/bill-geyer-ragr8q/15min`, a
  separate dedicated GK1 account (not Bill's personal one), wired into
  `index.html`'s "Get in touch" section above the form. One event type: a
  phone/Google Meet "touchpoint" call, Bill calls the attendee. Evenings/
  weekends only. The in-person first appointment is scheduled manually by
  Bill after the call, not self-service bookable.
- **Zoho Web-to-Lead — form-side synced, live test still pending.** Bill
  has generated and regenerated the Zoho Web-to-Lead form twice now (most
  recently 2026-07-29, to match the trimmed 4-item tech-interest picklist)
  and `#leadForm` has been diffed and kept current against each export
  (security tokens, analytics rid/tw, field names/values) — see
  `docs/decisions.md` "Lead form history" for the diff details. What's
  still missing: an actual end-to-end submission test once this is live
  on Spaceship.
- **Backlog: Cal.com bookings aren't captured as Zoho Leads** — no native
  connector yet. Options to check in order: Zoho Flow, Zapier/Make,
  Cal.com webhooks. Not yet researched.
- **Acknowledgement email**: planned via a Zoho CRM Workflow Rule on new
  Lead creation, should include the Cal.com link. Not yet built.

## Open checklist (priority order)

1. Zoho Web-to-Lead — form wired and kept in sync client-side (tokens,
   field values), not yet tested end-to-end with a real submission once
   this is live on Spaceship.
2. Add hero tagline line: "Solar · Battery Backup · Heat Pumps" /
   "Residential · Commercial" (not yet added to the site). Originally
   confirmed wording included "Generators" — dropped from this suggestion
   since generators were later removed as a residential offering entirely;
   don't reintroduce without a deliberate call.
3. *(Optional)* basic analytics — currently none.
4. Reminder for Bill (not a site task): once copy is finalized, sync his
   bio across the site, Recheck profile, and Cal.com profile.
5. Backlog: Google Business Profile (prioritize this — service-area
   business, no home address shown) + Facebook Business Page. LinkedIn
   explicitly ruled out — Bill wants GK1 kept low-profile relative to his
   W-2 employer, Ampt.
6. Cal.com→Zoho Lead sync (see above).

Bill is planning a broader round of content rewrites across both pages —
don't push anything live without confirming first.

## Other context

- A future solar estimator page (roof type + bill → calculation) was
  discussed and confirmed as a good idea but deliberately deferred — needs
  real backend logic, don't stub it in unprompted.
- **Separate, unrelated CRM build-out — not tracked in this repo.** Bill's
  Zoho CRM object design (Contact/Property/Lead fields, referral
  commissions) lives as its own handoff docs in Google Drive:
  `My Drive (bill@gk1.energy)\02_AREAS\Marketing_Brand\GK1-CRM-Decision-Handoff_*.md`.
  Pointer only — only relevant here if a task explicitly touches the
  CRM/lead-data side rather than the website itself.

## Adding to this file

Keep this file to current state + active conventions + pointers. When a
task produces new rationale, history, or a "here's why we chose X over Y"
writeup, put it in `docs/decisions.md`, not here — that keeps this file
cheap to load every session.
