# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I am the new PM for **Rook Dispatch** (started Mon 24 Aug 2026), reporting to
the Director of Product. Sources: rook-wiki (About Rook, Glossary, Team
directory, Releases, Q3 roadmap, Product briefs, Dispatch page), plus
`00-rook/company/notes/handoff-from-priya.docx`. Wiki pages are searchable by
title only; comments appear only via read_page.

### Company and products
- Rook Industries sells coordination/provisioning software to masked
  responders (independent, not employees) and their handlers/quartermasters.
  Subscription, priced per active responder. Founded 2014; HQ Site Aleph.
- **Rook Dispatch** (mine): availability, proximity, who gets pinged for a
  callout, and whether they take it. Handlers use the web console; responders
  use a native phone app. Monthly release train, 4.x numbering.
- **Rook Supply**: requisitions, maintenance, field failure reports.
  Handlers and quartermasters. Shares the Responder Availability Record
  (written by Dispatch, read by Supply).
- **Hard rule:** cover identities are never stored; Rook cannot and must not
  map them to legal identities (Security Policy 4.1). Never design for it or
  try to work out who anyone is.

### People (wiki comments use roles, not names)
| Role in comments | Person | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran, Site Aleph | Runs Dispatch eng. Priya's "start here". |
| Staff engineer | Wen Li, Berlin | Built the ping-ranking logic. No written doc. |
| Product designer | Sofia Marino, Site Aleph | Console + phone app; ran the September interviews. |
| Support lead | Nadia Hoffmann, Berlin | Owns tickets; has the ticket breakdown. |
| Director of Product | Helen Achebe, Site Aleph | My manager; owns roadmap and commitments. |
| Data analyst | Ravi Menon, Singapore | Weekly acceptance-rate reporting. |
| Priya | Priya Raghunathan | Previous Dispatch PM; left 21 Aug. Unavailable. |
Handlers interviewed by Sofia, 2-5 Sep (console redesign research): Aunt Dot
(Vesper), Mr. Ambrose (Captain Vantage), Halloran (Sgt. Bulwark; also runs
the gear cage, so he uses Supply heavily), Kip (Meteor Mite and The Gale).

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: one
  callout offered to one responder. Outcomes: **taken**, **turned down**,
  **missed** (ping wait expired). Turned down and missed both pass it on but
  are recorded separately.
- **Ping wait**: seconds before a ping counts as missed; same for everyone,
  set in the release, not a runtime setting.
- **Routing priority**: score ranking available responders. Inputs: proximity
  (travel-time estimate), availability, capability match, recent acceptance
  history. Declining or missing lowers recent acceptance, so lowers later rank.
- **Acceptance rate** (headline metric): pings taken / all pings.
  **Time-to-accept**: median seconds ping to taken. **Coverage gap**: no
  available responder had the needed **capability tags** (flight,
  structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management,
  de-escalation). A gap means nobody could go, not that nobody would.
- **Mutual aid**: responders covering for each other; unsupported, Q4 list.
- Supply: requisition, field failure report, service interval.

### Where things stand (as of 13 Oct 2026)
- **4.2 shipped 12 Aug and is the live problem.** It (1) weighted proximity up
  relative to recent acceptance history, and (2) cut ping wait 90 to 60 s.
  Since then callout tickets run ~3x normal. Support's split (26 Aug): about
  two thirds "phone never goes off", one third "gone before I could answer".
  Support explains the second by the 60 s cut; the first is unexplained.
- Marcus asked (14 Aug) whether the change applies to responders who turn jobs
  down too; config doesn't distinguish them. Unanswered: Wen Li was away,
  Priya left. Don't assume a decision was made.
- Priya's view: mostly seasonal ("August is always soft"), look in September,
  don't revert (the change was asked for). Marcus and Nadia agreed not to hand
  me a conclusion; a regroup on 4.2 was planned for after my first week.
- **rook-database findings (pings, callouts, tickets; 29 Jun - 6/7 Sep only,
  so no prior-year data and the seasonal claim can't be tested):**
  - Acceptance was flat at 75-78% for six weeks, then fell to 54% in the week
    of 12 Aug, 66% in the next two, 73% by week of 31 Aug. Missed pings went
    from 2-6 a week to 38, then 21-28. Tickets went from 5-8 a week to 20-32.
    Ping volume was flat (~170/wk) and no responder dropped out, so this is not
    lower demand. The step change lines up with the release, not a gradual dip.
  - **Four responders (Vesper, Meteor Mite, The Undertow, Farlight) nearly
    vanished from the ping order:** about 49 pings a week before, 43, 16, 6, 3
    after. Their post-release pings are mostly missed (acceptance ~20%). The
    other 12 absorbed the volume (123 to 162 a week). Their acceptance fell
    modestly (78% to ~74%), consistent with the 60 s cut. This matches "phone
    never goes off" (Farlight ticket 3060) and Kip's quiet Meteor Mite.
  - **The headline rate recovering to 73% is partly survivorship:** the four
    left the denominator. Acceptance rate alone hides this.
  - Callouts with no taker rose from 4-12 to 14-17 a week (7 in the partial
    last week); average pings per callout rose from ~1.23 to ~1.3.
  - Not known: why those four were missed first (no response-time or routing-
    score columns), whether they are far from callout areas, whether a missed
    ping lowering rank is a feedback loop that locks them out. These are
    hypotheses for Wen Li to confirm in the ranking code. Two changes shipped
    together, so effects of the 60 s cut and the weighting are not yet
    separated.
- **Roadmap is stale** (all rows last reviewed 30 Jun). Committed for 4.2 but
  absent from the 4.2 release notes: **Availability Confidence** and
  **Ping timeout tuning** (4.2 only had the flat cut; unclear whether that
  counts). Priya says items were squeezed out and the Director of Product
  conversation about which remain Q3 commitments "hasn't happened". Also
  **Requisition approval chains** is committed for 4.3 (Supply), and
  **Handler phone app** and **Shared cover between responders** are Q4
  exploring. No 4.3 appears in Releases yet. Changes to committed items go
  through Product.
- **Briefs**: Bulk Callout (Jan) and Routing Override Audit Log (Mar) are
  already shipped (4.1, 4.0); their pages read as unstarted, so they're
  stale. Handler Phone App (8 Sep) is exploring, owned by the designer, not
  staffed. Requisition Approval Chains (14 Jul) asks for a second approval
  over $2,000 but bundles several extra asks; scope needs cutting.
- **Gaps I owe**: written description of how pings are decided (Priya asked
  for it; Wen Li is the source); a regular 15 minutes with Nadia; the roadmap
  conversation with Helen. Console filter-persistence tickets are noise.
- **Interview evidence (4 handler pages read, anecdotal, no numbers):** three
  of four describe the "gone before I could answer" pattern as recent, in
  August. Two describe a split: Kip's Meteor Mite is quiet all week while The
  Gale "hasn't stopped"; Aunt Dot reports both quiet stretches and fast-
  vanishing ones. This is consistent with the 4.2 change concentrating
  pings, but it is a hypothesis to test, not a finding. Nobody interviewed
  asked about routing; the research was framed as console redesign.
- Not yet read: the rest of the Customer interviews database and the Research
  page. Ticket bodies after 19 Aug and the other 2 tables' details were not
  reviewed in full.

### How to work with me
- Cite the wiki page or person behind a claim; say when something is
  unverified or only from Priya's handover. Don't state a cause for the 4.2
  drop as fact until data supports it.

### Added at end of Module 1 session
- A draft of how pings are ranked is in `00-rook/company/notes/how-pings-are-ranked.md`; it has four questions still open for Wen Li (weights, penalty for missed vs turned down, any floor, effect of ping wait).
- Next data asks for Ravi: the four locked-out responders' response times before 12 Aug, and last year's Aug-Sep for the seasonal claim.
- The 24 Aug start date and "Halloran is a handler who runs the gear cage" are the points I corrected or inferred; confirm if they matter.
- Contradictions found across sources: Priya's "ask engineering for numbers" vs Ravi owning them; "monthly" releases vs Apr, Jun, Aug; roadmap statuses vs what shipped.
- This Working context is over the two-page target; the user chose to keep it as is.
- Module 2: support_tickets has 147 rows (29 Jun-7 Sep), sorted into quiet 30, gone-before-answer 15, saved filters 16, console 40, Supply 26, admin 14, phone 6. All 45 quiet/gone tickets are from 12 Aug on, none before; quiet:gone is 2:1, matching Support's 26 Aug split. Missed pings ran 2-6 a week (1-3%) before 12 Aug, then 38.
- The four interviewed handlers file almost no tickets (Aunt Dot, Halloran, Kip: 0; Mr. Ambrose: 1, on 13 Aug), so interviews and tickets cover different handlers. Vesper and Meteor Mite have no tickets at all; the quiet tickets are about Farlight, The Undertow, Corporal Ashgrove and Halfmoon, and the last two show only milder drops. No ticket complains of overload.
- Mr. Ambrose's half-dressed callout (ticket 3043) was the evening of 12 Aug, release day, not "two weeks ago" as he said in interview. Weighting: database for what happened, tickets for timing and frequency, interviews for what to ask next, none for cause.
- Open: Wen Li's ranking questions, now including whether a low recent-acceptance score can lock a responder out for good; last year's data from Ravi; whether handlers see race or sequence. Unsent drafts are in `00-rook/company/notes/handler-follow-up-interview-guide.md` and `drafts-wen-li-and-nadia.md`.
