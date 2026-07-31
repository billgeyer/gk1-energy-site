# GK1 Energy Site — Decision History

Rationale, sourcing trails, and the back-and-forth behind choices already
reflected in the live site. Read this when a task needs to know *why*
something is the way it is (e.g. "why does battery framing differ between
pages," "why was the multifamily angle dropped," "what's the sourcing for
the MA heat pump figures"). For current state and active conventions, see
`../CLAUDE.md` instead — that file is what loads every session; this one is
read on demand.

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
- **Battery framing is deliberately different between the two pages — not
  an inconsistency.** `index.html`'s "What I Offer" has a standalone
  "Battery Backup" tile because most residential buyers are shopping for
  resilience (keeping the lights on), and that wording also matches the
  lead form's "Solar panels + battery backup" checkbox.
  `business-solar.html`'s tile instead says "Battery Storage" and
  explains that commercial batteries are mainly about mitigating demand
  charges (peak shaving), with true outage backup for critical
  infrastructure normally being a separate standby generator — the
  battery there just absorbs load spikes, it doesn't carry the building.
  Don't "fix" this to match the residential wording; it's describing two
  genuinely different use cases.
- **Standby generators deliberately dropped as a residential offering on
  `index.html`.** Bill's call: generators run on fossil fuel, which reads
  as incongruent next to a solar/battery/heat-pump pitch built around
  "renewable," there are no state-level incentives for generators (unlike
  the other three), and the sales conversation for a generator is
  genuinely different from the other three. What I Offer went from 3
  tiles (Solar & Battery Backup combined, Heating & Cooling, Backup
  Generators) to 3 different tiles: **Solar** and **Battery Backup** split
  into their own tiles, **Backup Generators** dropped entirely. The
  Background & Credentials "Generator Contractor, Long Island, NY" tile
  was also removed, but that career history wasn't erased, it moved into
  the new Battery Backup tile as a credibility line ("I got my start in
  backup power at a standby generator company, so I understand critical
  loads and whole-home coverage..."), since that experience directly
  supports how Bill sizes a battery backup system, a better home for it
  than a standalone career-history tile. The "Generators" checkbox was
  also removed from `#leadForm`'s tech-interest list. **This was scoped
  to `index.html` only** — `business-solar.html` never offered generators
  as a product in the first place, nothing to change there for this
  reason specifically.
- **Terminology: "Heating & Cooling" is the section/tile label, "heat
  pump(s)" is the product term, used consistently everywhere else.**
  Matches how Mass Save itself structures the topic (their own site path
  is `.../heating-and-cooling/heat-pumps/...`, category then product).
  Don't use "mini-split" or "HVAC" as a competing term in visible copy,
  "mini-split" is just one installation style of heat pump and naming it
  separately undercuts single-term consistency; "HVAC" got swapped to
  "heat pump" in the Financing Loan tile for the same reason. `HVAC` is
  still fine inside the JS mandatory-field script text (Zoho-generated,
  not visible copy) and in code comments, that scope exclusion is the
  same one already established for the em-dash rule.
- **Multifamily & Rental Property angle deliberately dropped from
  `index.html`** (it used to be its own tile in a standalone Who I Serve
  section, built around the split-incentive problem: owner covers the
  capital cost, tenants on individual meters see the electric savings).
  Bill's call: landlord/rental economics aren't his current expertise right
  now, and keeping the angle in blurred an otherwise straightforward pitch.
  The site now covers single-family homeowners only. He may come back to
  landlords later if he builds that expertise; don't reintroduce the tile
  without checking first.
- **Financing section is deliberately equipment-agnostic, not solar-only.**
  Bill arranges financing for heat pumps and generators too (e.g. Team
  Sunshine's HVAC loan program in Massachusetts), so Cash Purchase and Loan
  are written generically. PPA and Lease stay solar-specific language
  though: PPA doesn't have an HVAC/generator equivalent, and Lease is
  explicitly flagged solar-first with a pointer to "comfort solution
  plans," the HVAC-world term for lease-style heat pump financing.
- **Word choice: "commercial" is reserved for citing actual external
  legal/tax-code terminology or established industry classifications**
  (e.g. "Section 48E," "commercial EPCs," a utility's "commercial rate
  class"), **never for describing GK1's own offering.** GK1's own copy says
  "business solar" / "business-scale," not "commercial solar" /
  "commercial-scale" — a deliberate marketing lane, not a legal distinction.
  See "Business Solar repositioning" below for the full history.
- **No em dashes in visible copy, site-wide.** Bill's explicit call ("makes
  it look like AI wrote it") — use a comma, a period splitting into two
  sentences, or a colon depending on what reads best, never a mechanical
  find-replace. Scope is reader-facing copy only; internal CSS/HTML code
  comments (invisible to visitors) were deliberately left alone. Title tags
  and footer/eyebrow separators use `·` instead. Watch for this drifting
  back in on future edits, since it's a stylistic tic that's easy to lapse
  into.

## Business Solar repositioning (business-solar.html)

`commercial-solar.html` was rewritten from "Commercial & Nonprofit Solar" to
"Business Solar" (new positioning and copy throughout: hero, nav CTA, tile
content, footer link text), and then the file itself was renamed to
`business-solar.html` to match, with every internal link across the site
updated (git history preserved via `git mv`). Key decisions, for context on
why the copy reads the way it does:

- **Audience test is the building and the bill, not the business type.**
  Bill was explicit: "It's all about qualifying the building, not the
  business, not the person, not the industry." The old "Who This Is For"
  section (5 segment cards: Professional & Industrial, Agricultural,
  Hospitality, Nonprofits, a Schools & Government exclusion) was **removed
  entirely**, not demoted, and replaced with three plain yes/no questions:
  is it owner-occupied, does it have a good roof, is the electric bill high
  enough to justify doing something about it. Anyone who doesn't fit is
  told to call anyway, no pressure either way.
- **Tax/incentive content** cites the federal Section 48E credit's
  Dec 31, 2027 placed-in-service deadline, plus 100% first-year bonus
  depreciation under current law, heavily caveated as general information
  (not tax advice) with an explicit "confirm with your accountant" line.
  The depreciation line later picked up "(under MACRS)" as a named term
  when the How This Works panel gained a paragraph mentioning MACRS
  depreciation schedules (see "Business Solar 2026-07-29 changes" below) —
  same underlying mechanism, just named explicitly once it appeared
  elsewhere on the page.
  **Deliberately does not mention** the earlier July 4, 2026
  "begin-construction" safe-harbor pathway to 2030, since independent
  verification (WebSearch, not just trusting a pasted AI summary) confirmed
  that deadline has already passed as of this repositioning — Bill's
  instruction was to drop it entirely as stale information, not explain
  that it closed.
- **CT/MA state-specific program numbers were kept out of the evergreen
  copy on purpose** (e.g. CT's NRES size brackets) since those figures are
  time-sensitive and expire; the state-by-state incentives section on
  `index.html` is the intended home for citable, sourced state program
  detail, and now has that content for all four states (see checklist #2
  in `../CLAUDE.md`).
- **File renamed**: `commercial-solar.html` → `business-solar.html`, closing
  out what had been an open question flagged more than once. The
  `?interest=commercial` query param value was deliberately left unchanged
  (it's internal/functional, not visible copy).

## Business Solar 2026-07-29 changes (scope, structure, Process)

Several changes landed on `business-solar.html` in one session, worth
recording together since they compound:

- **Landlord/commercial-tenant scope opened up.** The "Who This Is For"
  first question changed from a hard "Is it owner-occupied?" exclusion to
  "Do you control the building? Owner-occupied is the most straightforward
  deal. Landlords with commercial tenants are often viable too, depending
  on the lease structure." This reverses the spirit of the earlier
  owner-occupied-only positioning (see "Audience test is the building and
  the bill" above) — confirmed with Bill as intentional, not a slip from
  a hand-off doc missing context. The `og:description`/`twitter:description`
  meta tags initially weren't updated to match and had to be caught and
  fixed separately; check those tags whenever a scope/positioning change
  like this lands, they're easy to miss since they're invisible in normal
  browsing.
- **"What it actually delivers" split into two sections.** It used to be
  one section mixing product tiles (System Types, Battery Storage) with
  benefit tiles (Cost Savings, Sustainability & ESG, Tax Incentives) under
  one heading, which read as incoherent once actually reviewed. Split into
  a new "System Types" section (product/technical tiles) placed right
  after "Who This Is For," and a trimmed "What It Actually Delivers" that's
  now pure benefits.
- **Process expanded from 4 to 5 steps**: a "Letter of Intent and Deposit"
  step was inserted between Proposal and Site survey & engineering. Framed
  entirely from the prospect's perspective (what it protects them from —
  not locked into a contract before engineering confirms the numbers), not
  the EPC/developer's perspective (submitting interconnection applications,
  collecting deposits, executing binding agreements) — those EPC-side
  actions were deliberately excluded as out of scope for Bill's advisor
  positioning, don't reintroduce them without a deliberate call. The
  Proposal step's closing line was also rewritten to name the LOI as the
  actual next step instead of vaguely gesturing at "the site visit."
  Step 4 (Site survey & engineering) first paragraph was rewritten from a
  single "licensed technician visit" to an "engineering team" review with
  specific criteria (structural load, electrical service/switchgear,
  shading/orientation, interconnection, site/title) to better set up the
  feasibility-contingency payoff in the second paragraph.
- **Headshot added to the hero**, matching `index.html`'s hero-grid layout
  exactly (same CSS, copied verbatim) — reinforces the same
  independent-advisor trust signal that the residential page already had;
  the business page previously had no photo at all.

## Index.html section consolidation

`index.html` was trimmed from 11 sections down to 8 after Bill's critique
that it "reads like a novel." Three merges, each folding redundant or thin
content into an existing section rather than cutting the underlying ideas:

- **Who I Serve → What I Offer.** Once the Multifamily & Rental Property
  tile was dropped (see above), Who I Serve's remaining copy was nearly a
  duplicate of the hero lede (both said "homeowners deciding whether solar,
  battery backup, heat pumps, or a standby generator..."). Folded into What
  I Offer's intro instead of standing alone as its own section. The merged
  section still carries `id="serve"` since the hero's "Who I help" ghost
  button links there, don't rename that id without updating the hero CTA
  too.
- **Verified & Certified → Background & Credentials (4th tile).** How This
  Works already teases Recheck verification with a one-line trust strip and
  a link; a full second writeup in its own section right below Background &
  Credentials was true duplication, not just adjacent content. Added as a
  4th expandable tile there instead, with `id="verified"` moved onto the
  tile itself so the anchor still resolves. The section's h2 changed from
  "Three vantage points on the same industry" to "Where this experience
  comes from, and how it's verified" since it's no longer literally three
  items.
- **State-by-state incentives → sub-block inside Financing.** Both were
  "here's the external, sourced landscape" content. Financing kept its own
  section-head; the incentive tiles now sit under a plain `<h3
  id="incentives">` sub-heading after the tax-credit note, closing with one
  combined note-line instead of two separate ones. **The visual treatment
  of the 4 state tiles has gone back and forth, worth knowing the full
  history before changing it again.** Started as `<details>` accordions,
  redone as plain always-visible cards in a `.cards-2` grid when the
  content was still one sentence plus a link (accordion felt oversized for
  that little text), then changed back to `<details>` accordions once the
  content grew substantially (Massachusetts alone reached 3 paragraphs + 4
  sources), at which point the accordion treatment fit better and the
  "don't have to rebalance a 2-column grid every time a state gets added"
  argument started to matter. `.cards-2` was removed from the stylesheet
  after the second switch since nothing referenced it anymore, if a
  future card-style layout is needed again, it's a simple 2-column
  `display:grid` rule to re-add. **Read the actual content weight before
  picking a layout here**: thin content favors cards/always-visible,
  substantial content favors accordion tiles.

**Rate News stayed its own short section** rather than merging, on
purpose: Bill wants it as an urgency hook early in the page, right after
How This Works, not buried in the money-focused cluster near Financing.
Its original placeholder content moved out at first (that level of detail
was meant to live with the state-incentive tiles), but it later got real
content instead of staying a stub, see "Rate News sourcing" below for the
current New England rate-hike examples and the source-verification history
behind them.

**How This Works lost its `.contact-panel` box** in a later pass, to
match Rate News's plain, unboxed treatment right below it and reduce
visual weight. The Recheck trust-strip line (the one-line teaser, not the
full writeup in Background & Credentials) stayed in this section; it
earns its place here because How This Works is the first substantive
trust content after the hero, and a compact early signal is cheap
insurance for anyone who won't scroll as far as the fuller Background &
Credentials tile. Watch the width if this section gets edited again: the
Recheck line and the two intro paragraphs need matching `max-width` (58ch)
or they visibly misalign, that happened once already.

**Hero H1 rewritten** to stop duplicating the lede: the old H1 listed the
same products ("solar, backup power...") the lede immediately re-lists by
name. The new H1 leads with the plain-talk/insider-experience positioning
instead ("Home energy decisions, explained plainly by someone who's worked
inside the equipment industry."), leaving the specific product list and
the "I'm Bill Geyer" introduction entirely to the lede.

**Rate News's evidence collapsed into a single tile**, matching the
Background & Credentials pattern: the headline and "no contract, no
negotiation, no vote" framing paragraph stay always-visible (that's the
emotional hook), but the causes list, the state-by-state rate-hike
bullets, and the closing line all moved inside one `<details class="tile">`
titled "The evidence, state by state." Tradeoff worth remembering: anyone
who doesn't click won't see the actual evidence, just the headline and one
abstract sentence. Accepted deliberately, the headline alone still carries
real emotional weight, and the people most likely to click through are
exactly the ones checking "does this apply to my state," which is who the
evidence is for anyway.

**Background & Credentials tile title shortened**: "Residential Inverter &
Battery Manufacturer, Sales & Business Development" → "Inverter & Battery
Manufacturer Representative." The body now defines EPC on first use
("EPCs (engineering, procurement, and construction firms)") since it's
used without explanation elsewhere on the page.

## Rate News sourcing

Rate News's boxed card leads with the grid-problem causes (aging
infrastructure, data center demand, natural gas volatility — PJM capacity
auction pressure was cut from this list in the 2026-07-28 copy pass as
unnecessary throat-clearing, not because it's inaccurate), then a bulleted
list of approved (and one pending) New England rate cases: Unitil MA ~6%
(2026), NH Liberty 17.54% + Eversource 10.3% (2025), CT United Illuminating
~7-8% (2025), ME Versant Power ~23% (2025) plus Central Maine Power's
pending ~11% filing, each with its own inline source link. **Source links
were swapped 2026-07-28** from official docket/PUC filings (harder for a
general reader to parse) to readable news articles (Boston Globe, NHPR,
NBC Connecticut, Maine Public, Portland Press Herald) covering the same
rate cases — Maine has two source links since it cites both the Versant
and CMP filings separately. **New Jersey's rate-hike story was in this card at
first but was deliberately removed** at Bill's request, it's not his core
market, so the section now opens directly with the causes instead of an
out-of-region anecdote. (History, in case a similar out-of-region example
gets considered again: Bill's original NJ percentages needed a framing
correction before publishing, he'd attributed them to "all four utilities
raising rates the same month," but those numbers were actually Rep. Josh
Gottheimer's office's framing of the increase *over the past year*, not a
single-month action. Verified via WebSearch before publishing, same
discipline as the OBBBA tax content.) **This needs the same discipline
going forward regardless of region**: don't automate the sourcing, this is
a static site with no backend, and content meant to create urgency needs a
human judgment call on source authority each time it's refreshed. Update
periodically and always anchor to a linked, named source.

- **Long Island (added 2026-07-31)**, once Long Island became part of the
  stated service area (see "Networking landing page, vCard & ref code
  tracking" below): a Long Island entry was requested specifically for
  Rate News, not just the Financing tile. Two facts, both dated and
  sourced, not third-party aggregator claims: LIPA's board-approved 3.9%
  base rate increase for 2025 (~$7/month average household), sourced from
  a dated FOX 5 NY news article (avoided several stale 2014/2015/2016
  CBS/ABC7 "PSEG rate hike" articles that resurface in search results for
  generic queries, none of which were current); and PSEG Long Island's own
  published monthly Power Supply Charge history, which shows +13.23% in
  February 2026 and another +12.7% in March 2026, pulled directly from
  psegliny.com's own rate information page rather than a solar-installer
  blog restating the same numbers. Framed as "no control over it"
  volatility (matching the section's existing framing) rather than a
  single steady rate-case increase, since PSC is a monthly pass-through
  that swings both directions (it dropped again by August), unlike the
  fixed-in-place rate cases cited for the New England states.
- **Restructured into per-state tiles, 2026-07-31**: the "evidence, state
  by state" content used to be one long bulleted `<ul>` inside a single
  `<details class="tile">`, which Bill flagged as turning into "one long
  blob" once Long Island was added as a fifth entry. Converted to match
  the Financing section's existing pattern exactly: an `<h3>` + intro
  paragraph, then a `.tiles` div with one `<details class="tile">` per
  state, alphabetical (CT / Long Island / ME / MA / NH). The closing "the
  homeowners who locked in solar before their state made the next
  headline" line was kept verbatim, just moved from inside the old wrapper
  tile to a plain paragraph after the new tiles grid, so it still reads as
  the section's closing beat rather than getting buried inside one state's
  expandable content.
- **Header renamed "state by state" → "region by region", 2026-07-31**:
  Bill caught the inconsistency himself — the Rate News h3 said "The
  evidence, state by state" while one of its five tiles is titled "Long
  Island (East End)," not a state. Two ways to fix it: rename the tile to
  a state name (`New York (East End of Long Island)`, matching the
  Financing tile) or rename the header. Bill chose to keep the tile as
  `Long Island (East End)` — shorter, and matches how the rest of the
  site's copy already refers to the region — so the header changed to
  "The evidence, region by region" instead. The Financing section's
  "State-by-state incentives" heading was deliberately left alone: its
  New York tile is named after the state (`New York (East End of Long
  Island)`), so "state by state" stays accurate there.

## State incentive tile sourcing

All state incentive card content should be treated as a snapshot, not
evergreen: rebate amounts, caps, and per-ton rates in these programs
change yearly, so don't assume these figures are still current without
checking before citing them again.

**Ordering, 2026-07-31**: both this Financing grid and the Rate News
per-state tiles are alphabetical by state name (Bill's explicit call,
"Connecticut down"), not chronological or by when a state was added. New
state tiles should be inserted in alphabetical position, not appended.

- **Massachusetts** (solar/battery/tax-credit content): sourced from a
  Massachusetts-specific Ohm Analytics policy digest Bill provided, each
  item links to a primary `.mass.gov` or utility source, trusted as
  sufficient given the digest itself only cites official URLs.
- **Massachusetts** (heat pump detail, added later): sourced from a
  second, separate Bill-provided summary that ended with "AI responses may
  include mistakes" (unlike the Ohm digest). Because of that, the specific
  dollar figures ($8,500 standard / $16,000 income-qualified / $25,000 0%
  HEAT Loan, and the 2025→2026 standard-tier cut from $3,000/ton-$10,000 to
  $2,650/ton-$8,500) were independently WebSearch-verified against Mass
  Save's own program pages before publishing. **One correction made in the
  process**: Bill remembered the $16,000 figure as having dropped to
  $8,500, but those are two different tiers, $16,000 is the
  income-qualified cap and hasn't moved; $8,500 is the standard-tier cap,
  down from $10,000. The "rebates shrink, not grow" urgency framing he
  wanted is accurate, it just needed to be anchored to the right tier.
- **Connecticut, New Hampshire, Maine**: solar/battery content sourced
  from state-specific Ohm Analytics digests Bill provided (same
  official-source-linked format as the MA one). Heat pump content for all
  three wasn't in any Ohm digest (those are solar/storage/EV focused, no
  state's summary mentioned heat pumps), so it was independently
  researched via WebSearch and cross-checked against each state's own
  program page (energizect.com, nhsaves.com, efficiencymaine.com) rather
  than trusted from third-party HVAC contractor blogs alone.
- **New York (added 2026-07-31)**, scoped specifically to PSEG Long
  Island's territory, not New York State generally, since NY-Sun and Clean
  Heat rebate structure differ sharply by utility (ConEd/National Grid
  territories run different numbers entirely). Solar: the standard NY-Sun
  Megawatt Block rebate has been fully allocated on Long Island since
  2016, so the incentive story here leans on the 25% NY state tax credit
  (up to $5,000, sourced from the Department of Taxation and Finance's
  IT-255i instructions at `tax.ny.gov`, not a third-party aggregator),
  sales/property tax exemptions, and full retail-rate net metering, which
  matters more here than in the New England tiles given PSEG LI's
  above-average residential rates. The income-eligible $0.40/watt
  Affordable Solar adder (≤80% AMI) was verified against NYSERDA's own
  Long Island Dashboard page, not a solar-installer blog. Heat pump
  figures ($4,000 market rate / $5,000 disadvantaged-community or
  moderate-income / $7,500 low-income) came directly from PSEG Long
  Island's own Home Comfort heat pump rebate page, which administers NYS
  Clean Heat for the LI territory directly rather than routing through a
  separate NYSERDA portal like most upstate utilities do.

## Favicon / OG image implementation

The business-card icon (hexagon badge + lightning bolt mark, mint
`#47e0b8` hex, orange `#f2a33b` bolt) was copied from the separate
`gk1-business-card` repo into `gk1-energy-site/images/`
(`gk1-icon-transparent.svg` and `gk1-icon-navy-bg.svg`) and is wired in
three places on both pages:

- **Favicon**: navy-bg version, `<link rel="icon" type="image/svg+xml">`,
  stays visible on both light and dark browser chrome.
- **Nav-bar lockup icon** next to "GK1.energy": transparent version, since
  it blends into the nav's dark translucent background with no visible
  edge. `.nav-name` picked up `display:flex` and a `.nav-logo{
  height:1.6em; }` rule (sized up from an initial 1.3em, and the gap
  tightened from 8px to 4px, per Bill's feedback that it should read at
  similar size/weight to the "GK1" text and sit closer to the G) to align
  the icon with the text.
- **Open Graph/Twitter share image**: a new `images/gk1-og-image.png`
  (1200×630, the standard OG size), generated by rasterizing
  `gk1-icon-navy-bg.svg` to a 630×630 square via `sharp` (installed
  temporarily via `npx`/scratch dir, not a project dependency, this is a
  static site with no build step, nothing was added to the repo beyond
  the output PNG), then extending the canvas with matching navy
  (`#10182c`) padding on both sides. **Watch for this if regenerating**:
  the navy-bg SVG's background rect has rounded corners (`rx="48"`), so
  extending the canvas without first flattening transparency
  (`.flatten({ background: '#10182c' })`) leaves visible white gaps at
  the corners where the rounded rect meets the padding, that happened on
  the first attempt and had to be redone.

## Lead form history

- **File upload field — removed, not just deferred.** Zoho's Web-to-Lead
  file-attachment support is grayed out on Bill's current 15-day trial
  (paid editions only) — but separately, Bill decided it's not worth
  having regardless, since asking someone to dig up and upload a bill cuts
  against the site's low-pressure positioning. `#leadForm` no longer has
  an upload/dropzone field (nor the JS/CSS that supported it). In its
  place: a **"LOWEST monthly electric bill (rough estimate)"** dropdown
  (Under $100 / $100–149 / $150–199 / $200–299 / $300–399 / $400+ / Not
  sure — rationalized to non-overlapping bands; the original list had
  boundary values like 150/200/300 double-counted between adjacent
  options) — asks for the *lowest* month specifically so a summer-inflated
  bill doesn't skew the estimate. Don't reintroduce file upload later
  without checking in first; this was a deliberate choice, not a
  temporary workaround.
- **Street Address and City removed entirely from `#leadForm`** (not just
  made optional), per Bill's explicit call that the form was too long and
  felt like data mining. His own sales process starts with a phone call,
  not a site visit, he finds out where someone lives on that first call,
  so a full mailing address isn't needed at lead-capture time. Required
  fields are just First Name, Last Name, Phone, Email, State, and the SMS
  consent checkbox. Zip stayed as a single optional field (fast,
  low-friction geographic signal) rather than being cut too. Zoho's
  client-side mandatory-field JS (`checkMandatory7504064000000701086`) was
  updated to match, Street Address/City/Zip were removed from its
  `mndFileds`/`fldLangVal` arrays. **Zoho-side check: done.** Bill marked
  Street Address, City, and Zip as `aria-required="false"` on Zoho's own
  Web-to-Lead form builder and sent back the regenerated source; it now
  matches client-side validation exactly (same 6 mandatory fields: First
  Name, Last Name, Email, Phone, LEADCF53, LEADCF6). Confirmed by diffing
  Zoho's fresh export against `#leadForm`: field names/ids, the `LEADCF1`
  tech-interest values, `LEADCF52`/`LEADCF5`/`Lead Source`/`Lead Status`
  defaults, and the honeypot field all already matched, no other changes
  needed there. Two things were deliberately **not** copied from Zoho's
  regenerated export: (1) `returnURL` — Zoho's fresh default is bare
  `https://gk1.energy/`, but `#leadForm` intentionally keeps
  `https://gk1.energy/?submitted=true#contact` so the on-page "Thanks,
  that came through" message still fires; (2) Zoho's own multi-select
  `<select multiple>` markup for `LEADCF1` and bare state-code options for
  `LEADCF6` — the checkbox-group and `CT · Connecticut`-style labels are
  better UX and POST the identical wire format, so no functional risk in
  keeping that version. The two Web-to-Lead security tokens (`xnQsjsdp`,
  `xmIwtLD`) and the analytics script's `rid`/`tw` values *were* refreshed
  to match Zoho's new export, those aren't safe to diverge on.
- **Second Zoho sync, 2026-07-29**: Bill rebuilt the Web-to-Lead form
  again after the `techInterest` picklist got trimmed to four items (see
  above), and its `LEADCF1` `<select multiple>` options now exactly match
  the four checkbox values on `#leadForm`. Diffing the new export against
  `#leadForm` again found one real mismatch worth remembering: the
  "Not sure yet, just exploring" checkbox's `value` attribute had drifted
  to just `"Not sure yet"` (a leftover from before the picklist trim) while
  Zoho's Multi-Pick option value is the full `"Not sure yet, just
  exploring"` string — fixed to match exactly, since a mismatched value
  silently fails to map into the Zoho field rather than erroring visibly.
  Same pattern as before: `xnQsjsdp`/`xmIwtLD` and the analytics
  `rid`/`tw` were refreshed to Zoho's new values, `returnURL` and the
  checkbox-group/styled-`<select>` UX were deliberately kept as-is rather
  than reverted to Zoho's defaults. **Lesson for next time**: whenever
  Zoho regenerates the form, diff every `value` attribute on `LEADCF1`
  character-for-character against the fresh export, not just the option
  labels/count — a UX-driven checkbox value can silently drift out of
  sync with Zoho's picklist value while looking identical to a reader.
- Full current field structure (for whoever maps this into Zoho's
  Web-to-Lead form builder next): `firstName` / `lastName` (split, not a
  single Name field), `phone`, `email`, `state` (2-letter abbreviation via
  a `<select>`, New England + NY prioritized at top in alphabetical order
  (CT/MA/ME/NH/NY/RI/VT), a disabled divider option, then the rest fully
  alphabetical — NJ/PA/MD are in that rest-alphabetical group, not
  prioritized, despite an earlier version of this note claiming otherwise),
  `zip` (optional, 5-digit, numeric-patterned), four
  `techInterest` checkboxes sharing one `name` (Solar panels / Solar
  panels + battery backup / Heat pumps (heating & cooling) / Not sure
  yet — trimmed from six on 2026-07-29, per Bill's call that the picklist
  had grown too long for a low-pressure form. EV charger and Heat pump
  water heater were dropped: neither is featured anywhere else on the
  site (not a What I Offer tile, not mentioned in the hero or Process),
  so keeping them as checkboxes read as scope creep relative to what's
  actually pitched; someone who specifically wants either can still say
  so in the free-text "Anything else worth knowing" field. "Heat pumps
  (heating & AC)" was also relabeled to "Heat pumps (heating & cooling)"
  to match the site's established "Heating & Cooling" terminology
  convention (see "Terminology" above) — was seven with a Generators
  option before that, removed when generators were dropped as a
  residential offering entirely, see the standby-generator decision
  above — sentence case throughout (capitalize only the first word of
  each option), matching Bill's Zoho Multi-Pick field values so a future
  Web-to-Lead submission maps correctly) — a multi-select, not
  single-select, so more than one can be checked — `secondOpinion`
  (optional checkbox),
  `referredBy` (optional), hidden `refCode` and `propertySegment`
  (silently set to `"commercial"` via JS when arriving from
  `business-solar.html`'s `?interest=commercial` link — replaces the old
  single-dropdown prefill logic), `lowestBill`, `message`, and the
  required `smsConsent` checkbox. Zoho's multi-select checkbox handling
  may need a specific `name`/`value` convention once the Web-to-Lead form
  is generated — check what Zoho outputs for a multi-select picklist
  field before assuming `techInterest` as-is works.

## Networking landing page, vCard & ref code tracking (2026-07-31)

Originated from a hand-off doc (`GK1-ClaudeCode-Handoff_NetworkingPage-vCard-RefCodes.md`)
prepared in a separate planning chat. Several details in that doc were
stale against the live repo and had to be reconciled before building
anything — repo state won in every case, per Bill's explicit instruction:

- Doc assumed file names `bill-geyer-solar-energy.html` (now `index.html`)
  and `bill-geyer-business-solar.html` (actually `business-solar.html`,
  no `bill-geyer-` prefix per this repo's naming convention) and referenced
  a `bill-geyer-trade-partners.html` page that doesn't exist anywhere in
  this repo. Ignored; not acted on.
- Doc assumed an automated "GitHub Desktop → cPanel Git Version Control
  pull" deploy pipeline. Actual deploy process is still fully manual
  (cPanel File Manager upload, see Hosting section in `CLAUDE.md`) — built
  the files for Bill to upload the normal way, no pipeline changes made.
- Doc's vCard spec said "leave phone/email as placeholders" but then
  hard-coded `bill@gk1.energy` as the placeholder value anyway, and both
  the phone and email were already public in the site footer. Used the
  real values directly (`(978) 358-1296`, `bill@gk1.energy`) rather than
  writing bracketed placeholder text into a file Bill would have had to
  hand-edit before it was usable.
- Doc's vCard `NOTE` field mentioned EV charging, which isn't and has
  never been an offering on this site (same category as the removed
  Generators option, see "Terminology" and the standby-generator decision
  elsewhere in this doc). Dropped from the note rather than reintroducing
  scope the rest of the site doesn't support.

**Geographic scope decision**: Bill has family (particularly in Southold)
on the East End of Long Island and is a lawyer with a New York/Palm Beach
client base, and wanted to extend GK1's stated service area to follow his
actual sphere of influence rather than ruling family/network contacts out.
Decision made to go with the fuller build-out (not just soft "relationships
beyond the region" hedge language): added a real, sourced New York
incentive tile (see "State incentive tile sourcing" above) and updated
service-area copy site-wide (meta descriptions, hero eyebrow, footer, and
the "outside that area" hedge line on both `index.html` and
`business-solar.html`) to read "New England & the East End of Long
Island." Deliberately scoped to "East End of Long Island," not "Long
Island" broadly or "New York" — matches Bill's actual local knowledge and
avoids implying coverage of Nassau/NYC-area territory with entirely
different utilities and incentive programs. Palm Beach was explicitly left
out — Bill spends winters there but isn't running GK1 activity there, so
no copy or content changes were made for Florida.

**`hello.html` / `bill-geyer.vcf` build**: styled by borrowing (not
redefining) `index.html`'s existing CSS variables, font imports, and
`.btn-primary`/`.btn-ghost` button classes — copied the literal values in
since `hello.html` is a single small file with no shared stylesheet to
import from. Deliberately excluded from both pages' nav — it's a
QR-code-only destination, not part of normal site browsing. Ref passthrough
uses plain `URLSearchParams` against `window.location.search`, same
approach already used on `index.html`, unaffected by the `#contact` hash
fragment.

**Ref code naming convention** (from the hand-off doc, adopted as-is,
no repo enforcement mechanism, just a documented human convention):
`[source]-[who/where]`, all lowercase, hyphens only —
`soi-[firstname-lastinitial]` for sphere-of-influence/personal contacts,
`dh-[town]` for door hangers, `flyer-[event]-[yr]`, `biz-[businessname]`
for stacks left at a business, `tp-[firstname-lastinitial]` for trade
partner referrals, `camp-[channel]-[month-yr]` for paid/campaign, append
`-2`/`-3` for repeat batches from the same source. These populate the
hidden `refCode`/`LEADCF3` field already wired into `#leadForm`; the Zoho
Referral object where fee structure and terms actually get logged is part
of the separate CRM build-out (see "Other context" in `CLAUDE.md`), not
this repo.

**Known open item**: `gk1.energy/hello` (no `.html`) won't resolve — this
repo has no `.htaccess`/rewrite config, and none was found during this
session. QR codes should target `gk1.energy/hello.html` explicitly unless
Bill confirms cPanel-side URL rewriting is configured, in which case this
note should be corrected.

**`download` attribute removed from the vCard button, 2026-07-31.** The
original hand-off doc specified `<a href="bill-geyer.vcf"
download="bill-geyer.vcf">`, which was implemented as written and deployed.
Bill tested it live: the `download` attribute forces a raw file download
into the phone's Downloads/Files app on every platform, rather than the
"Add Contact" native preview screen he expected (and that's the actual
selling point of a vCard: someone reviews and commits it, they don't dig a
.vcf out of Downloads to import manually). Removed `download` from the
`<a>` so the browser follows the file's `Content-Type` header instead.
Confirmed locally that a plain static file server returns `text/x-vcard`
for `.vcf` with no extra config, and Apache's stock `mime.types` (which
cPanel uses) maps `.vcf` the same way, so this should carry over to
production, but it's worth Bill re-testing on his phone after the next
upload to confirm the native "Add Contact" screen actually appears, since
MIME handling can still vary by hosting config or browser.

**Superseded same day: on-page contact card added instead of relying on
native vCard preview.** Bill's actual complaint wasn't the download
mechanism specifically, it was that tapping "Save my contact info"
produced friction with no chance to see what they were getting before
committing. Relying on the OS to show a native "Add Contact" screen for a
correctly MIME-typed `.vcf` (the fix above) is real but inconsistent
across browsers and in-app browser webviews (Instagram/LinkedIn in-app
browsers, some Android Chrome configurations, etc. don't always honor
`text/x-vcard` the same way iOS Safari does), so it wasn't a reliable
fix for "let them review before they commit" on its own. Added a
`.contact-card` block directly on `hello.html`, always visible before the
buttons, showing name, title/org, and tappable `tel:`/`mailto:` links for
phone and email, so the preview no longer depends on OS/browser vCard
handling at all. With that in place, the `download` attribute was added
back to the vCard button (`Save to my contacts`), since forcing a direct
save is now fine, the person has already seen the info on the page before
tapping it.

**Business-card tagline added to the contact card and vCard NOTE,
2026-07-31.** Bill wanted the on-page preview to actually read as a mini
version of his physical business card, not just name/phone/email. Added a
`.tagline` line to the `.contact-card` (styled like the site's eyebrow
labels, IBM Plex Mono, small caps) reading "SOLAR · BATTERY BACKUP · HEAT
PUMPS · RESIDENTIAL · COMMERCIAL" — matches the exact wording from the
still-open hero-tagline checklist item in `CLAUDE.md`. Also folded the
same tagline into `bill-geyer.vcf`'s `NOTE` field, ahead of the existing
service-area sentence, so it's visible in the phone's contact manager
after saving, not just on the page before saving. Used middle-dot
separators (`·`) instead of commas deliberately: vCard 3.0's TEXT-value
grammar technically requires commas/semicolons to be backslash-escaped,
and switching to `·` sidesteps that entirely rather than relying on every
contacts app's parser to be lenient about it.
- **Also fixed in this pass**: the hero-photo captions on `index.html` and
  `business-solar.html` said "Bill Geyer / Energy Advisor, GK1 Energy",
  missing "Independent" that's used everywhere else on both pages (title
  tags, meta descriptions, hero lede, photo alt text). Bill caught this
  himself; added "Independent" to both captions rather than removing it
  elsewhere, since "independent, not installer" is a deliberate site-wide
  positioning point (see "Active conventions" in `CLAUDE.md`).
- Also dropped "free" from `hello.html`'s subhead ("request a
  consultation" instead of "a free consultation") — Bill's call, read as
  slightly salesy for an already low-key page.

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

## Session tie-off, 2026-07-29 ~10:00 AM ET

Everything above through the "Business Solar 2026-07-29 changes" section
and the second Zoho sync note was verified against the actual live site,
not just the repo, as of this timestamp: both pages were uploaded to
Spaceship, the mobile nav overflow bug was fixed and reverified, the lead
form's tech-interest picklist was trimmed and re-synced with Bill's
regenerated Zoho form, and Bill submitted a real test lead that landed
successfully. `CLAUDE.md` carries the same tie-off marker. A future
session picking this up should check `git log` for anything past this
point before assuming either doc is still current.
