# How Rook Dispatch ranks responders for a ping

Draft, 13 Oct 2026. Written from the wiki (Glossary, Rook Dispatch page, 4.2
release notes) and the rook-database. The ranking code has not been read.
Items marked **unconfirmed** need Wen Li (Staff Engineer, who built it).

## 1. A callout comes in
A handler enters it, or an intake system pushes it. Dispatch ranks every
available responder for that callout and produces a routing priority order.

## 2. The ranking
Each responder gets a routing priority score from four inputs:
- **Proximity**: a travel-time estimate, not straight-line distance (since 4.1).
- **Current availability**: whether they are available for callout now.
- **Capability match**: whether their capability tags cover what the incident
  requires.
- **Recent acceptance history**: how often they have recently taken pings
  rather than turned them down or missed them.

Since 4.2, proximity carries more weight relative to recent acceptance
history. The exact weights and how far back "recent" reaches are
**unconfirmed**.

## 3. The ping
The top-ranked responder gets a ping on their phone. They can take it, turn it
down, or let it time out. The ping wait is 60 seconds since 4.2, down from 90.
It is set in the release and is the same for everyone.

## 4. If it isn't taken
The ping moves to the next responder in the order. A taken ping assigns the
incident and marks the responder engaged.

## 5. The feedback loop
Turning down or missing a ping lowers that responder's recent acceptance
component, so they rank lower on later callouts. The Glossary describes both
outcomes as having this effect. Whether the effect compounds is **unconfirmed**.

## What the data suggests (hypothesis, not finding)
- Marcus Oyelaran asked on 14 Aug whether the 4.2 weighting applies to
  responders who have been turning jobs down. The config doesn't distinguish
  them. Nobody answered.
- After 12 Aug, four responders (Vesper, Meteor Mite, The Undertow, Farlight)
  went from about 49 pings a week to 3, and most of their remaining pings were
  missed. That fits a loop where missing lowers rank, which means fewer pings,
  which means more misses.

## Questions for Wen Li
1. What are the actual weights and the recent-history window, before and after
   4.2?
2. Is a missed ping penalized the same as a turned-down one, and does the
   penalty decay?
3. Is there a floor that keeps any available responder reachable?
4. Does the ping wait affect the score itself, or only when the ping moves on?
