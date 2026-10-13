# Handler follow-up interview guide (Dispatch / 4.2)

Purpose: test, without leading, whether handlers' experience matches the 4.2 pattern in rook-database (some responders' pings nearly vanishing, others absorbing volume, pings gone faster). This is a hypothesis, not a finding.

Source: Customer interviews database (rook-wiki), 2-5 Sep 2026, run by the product designer (Sofia Marino) as console redesign research. Nobody was asked about routing. Evidence so far is anecdotal.

## Ground rules
- Ask for dates, counts and specific incidents. Do not mention 4.2, the 60 s ping wait or ranking weights.
- Never ask anyone to identify a responder outside the console (Security Policy 4.1).
- Ask Sofia to lead, or join her. Ask Nadia whether support has tickets from these handlers.
- Keep Halloran short. His console use is light, and his Supply complaints go to the Supply owner.

## All four
1. Can you pull up the last few callouts your responder was offered, roughly when each came in, and whether they took it? A phone or console history is fine.
2. When did you first notice a change, and what was the first thing you noticed?
3. Did your responder's busy or quiet pattern change at any point this summer, and when?

## Aunt Dot (Vesper) - priority
Vesper is one of the four responders whose pings nearly vanished after 4.2 (rook-database).
1. You mentioned quiet stretches. Roughly when did they start and how long did they last? What was different about the busy weeks?
2. When a callout comes in, about how long between the buzz and him getting a thumb on it? Is he usually reachable straight away?
3. Does he ever turn jobs down on purpose? Has that changed lately?
4. Has he heard from his own contacts about other responders being quiet or busy?

## Mr. Ambrose (Captain Vantage)
1. The boot-half-on incident was about two weeks before 2 Sep. Do you remember the day, and how long he had between the alert and it moving on?
2. You said a slower response used to still land him the job. About when did that stop being true?
3. Roughly how often is he offered callouts, and has that changed?
4. Is he usually near where callouts happen, or often further away?

## Halloran (Sgt. Bulwark) - keep short
1. Can you ask Bulwark for the date of that callout and how long he thinks he had?
2. Does he get offered callouts steadily? Same volume as before August?
3. Does he turn jobs down, and has he changed how he handles them?

Pass on to the Supply owner (not Dispatch): requisition approval took 11 days for a cracked vest plate with the priority field having no effect; failure reports "go into a void"; catalog search needs category filters.

## Kip (Meteor Mite and The Gale) - priority
Meteor Mite is another of the four whose pings nearly vanished (rook-database).
1. When did Meteor Mite go quiet, and roughly how many callouts a week did they get before that?
2. Did Meteor Mite do anything different around then (moving, changing hours, turning jobs down)?
3. How often are they offered a callout and miss it, compared with before?
4. How are The Gale's callouts going? Is the exhaustion about volume or about the hours they land at?
5. Is the quiet / on-fire split still happening, or has it eased since 4 Sep?

## Added after re-reading the first round

**Prompted vs unprompted.** In round one, some mentions only came after the interviewer asked. Aunt Dot's quiet weeks came after "weeks where it feels too quiet rather than too fast?" ("Now that you mention it"), and Halloran's callout mention came at the end of an "anything at all?" question. Kip's quiet/busy comparison, Ambrose's boot incident and Dot's lost race were volunteered. In round two:
- Start open ("tell me about the last week or two of callouts") and note what they raise before any prompt.
- Only then ask directly about quiet weeks and fast-vanishing callouts, and record which were prompted.
- Ask Aunt Dot and Halloran to re-describe in their own words, with dates, before any prompt.

**Race or sequence?** Handlers describe a race ("phone to stairs", "it went to somebody else"), but the glossary says a ping is offered to one responder at a time and passes on when missed or turned down.
- Ask handlers: what do you see on the console when a callout is offered, and when it moves on? What tells you it has moved on?
- Do not explain how pings work. Confirm the mechanism with Wen Li (see how-pings-are-ranked.md).

## What to do with the answers
- Compare dates with the 12 Aug release and the weekly acceptance / missed-ping numbers.
- Cross-check against Ravi's data asks (response times before 12 Aug for the four locked-out responders; last year's Aug-Sep).
- Confirm mechanisms with Wen Li (see how-pings-are-ranked.md), not with handlers.
