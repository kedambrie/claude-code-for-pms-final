# Drafts: note to Wen Li, message to Nadia

Drafted 13 Oct 2026. Not sent. Check the numbers against rook-database before sending.

## 1. To Wen Li Staff Engineer (Berlin)

Subject: Four questions on how pings are ranked, and one on lockout

Hi Wen Li,

I'm the new PM for Dispatch. I'm trying to understand why some responders stopped getting pings after 4.2, and you're the only person who can confirm how ranking works. I've written up my understanding from the wiki and the database (attached: how-pings-are-ranked.md). It's a draft and I haven't read the code, so please correct anything wrong.

What I'm seeing, in plain terms:
- Four responders (Vesper, Meteor Mite, The Undertow, Farlight) went from about 49 pings a week before the 12 Aug release to about 3 now. Most of what they do get is missed.
- Support tickets back this up. Farlight's and The Undertow's handlers have each filed 10+ tickets since 17 Aug saying their phone "has not gone off" for 3 to 9 days.
- Acceptance among the other twelve fell only a little, which fits the 60 s cut.
- This is a pattern, not a finding. I haven't tested a cause.

Questions:
1. What are the weights for proximity, availability, capability match and recent acceptance, and how far back does "recent" go? Before and after 4.2?
2. Is a missed ping penalised the same as a turned-down one, and does the penalty decay over time?
3. Is there a floor that keeps an available responder reachable, or can a low recent-acceptance score leave them out of the order altogether?
4. Does the ping wait affect the score itself, or only when the ping moves on?
5. Can a responder with a low score get so few pings that they can't recover, even if they respond promptly now?

Marcus asked on 14 Aug whether the 4.2 change applies to responders who turn jobs down as well, and I couldn't find an answer. Do you know if it does?

I can work around your time. Even a short call, or a pointer to where the logic lives, would help. I'd like to bring something to the 4.2 regroup. I'm not asking you to change anything.

Thanks,
[name]

## 2. To Nadia Hoffmann Support lead (Berlin)

Subject: 4.2 tickets, and a quick catch-up

Hi Nadia,

I'm the new PM for Dispatch. Two things.

1. I've been through the support tickets from 29 Jun to 7 Sep. Since 12 Aug, 45 of 107 tickets are about two things: responders gone quiet (30) and pings gone before the responder could answer (15). That matches your 26 Aug split, about two thirds and one third.
   Farlight's and The Undertow's handlers have each filed 10+ tickets, with the latest saying "I do not know what to tell her." Have they had a reply? If not, a short honest one would help, such as "we've seen the pattern and are looking into it". I'd avoid giving a cause until we know it.
2. Two responders in the database pattern, Vesper and Meteor Mite, have no tickets at all. Their handlers (Aunt Dot, Kip) told us about it in interviews. Have either got in touch some other way, such as calls or chat?

Could we also set up a regular 15 minutes? I'd like to see your ticket breakdown and hear what you're hearing from handlers.

Thanks,
[name]
