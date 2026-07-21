# GK1 Energy Site

Static marketing site for Bill Geyer / GK1 Energy — an independent energy advisor
(solar, battery storage, heat pumps, generators). Two hand-coded HTML pages, no
build step, no framework.

Mental model: the site is designed as an extension of Bill's business card (see
"Site strategy" below) — most visitors will already know who he is before they
land here. It's not optimized for cold organic search traffic.

## Pages

- `index.html` — residential site, lives at the site root (`gk1.energy/`).
  Sections top to bottom: hero (headshot + headline) → How This Works (+
  Recheck trust strip) → Who I Serve → What I Offer → The Process (4 steps) →
  Background & Credentials → Verified & Certified (full Recheck writeup) →
  Financing (4 ways to pay) → State-by-state incentives (CT/MA/NH/ME — still
  stub content) → Get in touch (the lead form, `#leadForm`).
- `commercial-solar.html` — commercial & nonprofit site
  (`gk1.energy/commercial-solar.html`). Sections: hero → How This Works → Who
  This Is For → What It Delivers → The Process (commercial-flavored, 4 steps)
  → Get in touch. Its CTAs route to `index.html`'s shared contact form via
  `?interest=commercial#contact`, which `index.html` reads via JS to prefill
  the interest field.
- Almost every major section on both pages ends with a short contextual
  "Let's talk it through →" line linking to the contact form — this was a
  deliberate fix for the long single-page scroll. When adding a new section,
  add one of these too, phrased for that section's topic (see existing ones
  for the pattern/tone).
- `images/` — site assets (currently just the headshot). Not committed
  casually; keep images compressed (<500KB) before adding.

Naming convention: keep `index.html` at the root (best for SEO/bookmarks — a
deliberate choice, not an oversight). New sub-pages should use plain,
description-based slugs (e.g. `commercial-solar.html`), not
`bill-geyer-*`-style filenames — cleaner URLs were an explicit ask.

## Site strategy (why the copy reads the way it does)

- Positioning is deliberately anti-pushy-solar-sales: "independent," "not
  shopping the market," "I'll tell you honestly if a quote is fair." Bill is
  an advisor who places projects with regional EPC partners — he does not
  design/engineer/install himself. Copy should never imply otherwise (e.g.
  the Process sections say "my installation partner handles..." not "I
  handle...").
- Trust/verification (Recheck) is a first-class element, not a footnote —
  the target audience is explicitly wary of solar sales tactics.
- Financing content stays general/educational (cash, loan, PPA, lease) —
  never cite a specific lender's rates, FICO minimums, or program terms as if
  they're Bill's own offer, since he isn't bound to one EPC's negotiated
  partner terms and those numbers go stale fast.

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
- **Operating procedure**: commit and push after essentially every change,
  even small ones — Bill's only copy of this work lives on one laptop, so git
  push is the off-machine backup. Confirmed as standing practice.
- **IMPORTANT — live site is stale**: as of the last session, gk1.energy has
  only ever received the very first round of manual uploads (filename
  rename, broken-link fix, phone number). Everything since then — Recheck
  section, Process sections, headshot, Financing section, contextual CTAs —
  exists only in git/GitHub, **not** on the live site. Don't assume gk1.energy
  reflects the current repo state; check with Bill before referencing "what's
  live."

## Contact info

- Footer phone number: `(978) 358-1296` (Google Voice number for GK1),
  wired as a `tel:+19783581296` link in both page footers.
- Email: `bill@gk1.energy`.

## Open checklist, roughly in priority order

**Sequencing note**: Bill's actual stated priority right now is Zoho
Web-to-Lead wiring (#1 below) **then** business cards next, since printing
and shipping takes several days and he doesn't want that on the critical
path. Items #3 (CTA phrasing) and #6 (QR destination) below are what's
actually blocking the card design from being final — worth resolving those
two before he goes to order, even out of strict priority order.

1. **Lead form has no backend.** `#leadForm` in `index.html` is a client-side
   placeholder (see the JS comment near the submit handler) — submissions
   currently go nowhere. Highest-priority gap; nothing else matters if a real
   visitor's form fill vanishes.
2. **CT/MA/NH/ME incentive tiles are still stub/placeholder copy** (visible
   `[bracketed placeholder]` text) — needs real state-specific content and
   source links, or the section should be hidden until ready.
3. **CTA phrasing inconsistency**: the decision was to standardize on
   "Request a Consultation" everywhere (site + business card + QR tag,
   replacing "free estimate"). `index.html` mostly already uses this;
   `commercial-solar.html` still says "Get in touch" throughout — not yet
   reconciled.
4. Add a compact, scannable "what I do" line near the top of the hero
   (Solar · Batteries · Heat Pumps · Generators / Residential · Commercial),
   mirroring the business card tagline — not yet done (we added the
   headshot instead, this is still separate/outstanding).
5. Add a favicon + Open Graph/Twitter card meta tags — needed before links
   get shared via text/QR/social, currently missing entirely.
6. Decide the QR code destination (likely a deep link straight to
   `#contact`) — lower urgency until the physical card is being finalized.
7. *(Optional)* basic analytics — currently no tracking at all.
8. **Reminder for Bill, not a site task**: once all the copy on the site is
   finalized, update his bio to match on **both** his Recheck profile
   (recheck.co) and his Cal.com profile — keep all three (site, Recheck,
   Cal.com) consistent. Bill does this himself, no site access needed.
9. **Backlog: standalone "already have a quote?" second-opinion CTA**,
   residential page (`index.html`) only. Right now this angle only exists
   buried inside the "Single-Family Homeowners" accordion tile and as one
   option in the contact form's dropdown — neither is a prominent, direct
   path for someone who already has a competing quote and wants a second
   opinion. That's a distinct (often more skeptical, further-along)
   audience from the main funnel and probably deserves its own visible
   line/section, not full copy yet — flagged as backlog, not urgent.

Bill is planning a broader round of content rewrites across both pages;
don't push anything live without confirming first.

## Lead capture & scheduling architecture

- **CRM**: Zoho CRM (standard plan), via direct **Web-to-Lead** integration —
  no middleman automation tool (n8n was considered and deliberately rejected
  as overkill for current lead volume/complexity). Bill needs to generate
  the Web-to-Lead form inside Zoho CRM (Setup → Developer Space → Webforms)
  and send the generated HTML/field mapping back so the existing styled
  `#leadForm` can be rewired to POST to it.
- **File upload field — removed, not just deferred.** Zoho's Web-to-Lead
  file-attachment support is grayed out on Bill's current 15-day trial
  (paid editions only) — but separately, Bill decided it's not worth
  having regardless, since asking someone to dig up and upload a bill cuts
  against the site's low-pressure positioning. `#leadForm` no longer has
  an upload/dropzone field (nor the JS/CSS that supported it). In its
  place: a **"LOWEST monthly electric bill (rough estimate)"** dropdown
  (Under $100 / $100–150 / $150–200 / $200–300 / $300–400 / $400+ / Not
  sure) — asks for the *lowest* month specifically so a summer-inflated
  bill doesn't skew the estimate. Don't reintroduce file upload later
  without checking in first; this was a deliberate choice, not a
  temporary workaround.
- **Acknowledgement email**: to be handled by a Zoho CRM Workflow Rule
  (Setup → Automation) firing on new Lead creation — not a separate tool.
  Should include the Cal.com booking link.
- **Cal.com**: a **separate, dedicated Cal.com account for GK1 Energy**
  (not Bill's existing account, which is set up for a different, unrelated
  use case) — connect Bill's other calendars (day job, personal, existing
  Cal.com account's calendar) purely for conflict-checking; new GK1
  bookings write to their own destination calendar. Only **one event type**
  is needed: a phone/Google Meet "touchpoint" call, with Cal.com's
  "Phone Call" location type configured so **Bill calls the attendee**
  (not the reverse) — avoids conference bridges/PINs, which was a
  deliberate choice for an older/less-tech-comfortable audience. Bill
  should place the call from his existing Google Voice number (already
  public on the site) for caller-ID consistency. Availability should be
  evenings/weekends only (Bill has a day job). The actual in-person first
  appointment ("SIT1") is intentionally **not** self-service bookable —
  Bill schedules that manually after the initial call, once he knows the
  lead's location and can judge drive time himself (his home base means
  drive time varies hugely — e.g. Newburyport MA vs. Fairfield County CT
  — and evening/weekend slots are scarce given the day job).
- **Cal.com — implemented.** Booking link is
  `https://cal.com/bill-geyer-ragr8q/15min`. Wired into `index.html`'s
  "Get in touch" section as a note-line above the form ("Already know you
  want to talk? Book a 15-minute call directly →"), so it's the first
  thing visible when reaching that section, before the longer form. Since
  commercial visitors also route to this same `#contact` section via
  `?interest=commercial`, they see it too — no separate commercial-page
  implementation was needed.
- **Zoho Web-to-Lead — still pending.** This is the one piece of the
  architecture not yet implemented; waiting on Bill to generate the
  Web-to-Lead form in Zoho CRM and send back the details (see above).
- **Backlog: Cal.com bookings aren't captured as Zoho Leads.** The website
  form and Cal.com are two separate systems — someone who books directly
  via Cal.com never touches the Web-to-Lead form, so no Lead record gets
  created for them. Unlike the form, there's no native direct-submit path
  for this, so some connector is genuinely needed (not optional
  complexity). Options to check, in order: (1) Zoho Flow, since Bill's
  already on Zoho CRM and it may support Cal.com as a trigger app; (2)
  Zapier or Make as a fallback — both have mature Cal.com triggers and
  Zoho CRM "create Lead" actions; (3) Cal.com webhooks feeding something
  custom, as a last resort. Not yet researched which of these Cal.com/Zoho
  actually support — flagged for later, not blocking anything else.

## Do not use: Helio Solar internal finance training PDF

Bill has (or may again) share a PDF titled "Helio Solar Finance Training
Guide" for reference. It is marked **Confidential — Internal Use Only** on
every page — it's Helio's internal sales-rep training material (compliance
scripts, specific lender partner terms/FICO minimums/contacts for GoodLeap,
Sungage, Palmetto LightReach, Climate First Bank, CT Green Bank, EnFin).
Decision made: **do not pull lender-specific details, contacts, or sales
scripts from it into the public site** — it's not Bill's to republish, the
numbers are Helio-specific (Bill works with multiple EPCs, not just Helio)
and go stale fast, and some of it is legally load-bearing for Helio's own
sales compliance, not general education. The site's Financing section
already covers the general (safe, public-knowledge) four-methods framework;
that's the ceiling for this topic unless Bill decides otherwise.

## Other context

- A Google Drive connector was set up mid-session but a specific shared
  folder wasn't accessible under the connected account; Bill deferred fully
  configuring it and used local file paths instead. May be worth revisiting
  if he wants to pull assets from Drive regularly.
- A future third page for a deeper solar estimator tool (roof type + bill
  amount → calculation) was discussed and confirmed as a good idea, but
  explicitly deferred — it needs real backend logic, out of scope until
  Bill says otherwise. Don't stub it in unprompted.
