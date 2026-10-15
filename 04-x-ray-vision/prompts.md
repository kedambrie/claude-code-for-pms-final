# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

Can you summarize any code changes that may have occurred around the 4.2 time?

### 2.

how might the proximity changes in 4.1 affect the responder

### 3.

What do you suggest as next steps in looking at this code?

### 4.

The pings table on rook-database has last session's numbers. Read that alongside this code. Does it back up what I found in Lab A? And does that answer the engineering manager's question above?

### 5.

Any hypothesis from you on what the root cause is>

### 6.

Do we have any data on average answer time (how long it takes a responder to answer a ping)?

### 7.

Is there any confirmation anywhere that the 4.2 was pushed to all responders?

### 8.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 9.

Somebody has been quiet for a month. Walk me through, step by step, exactly what would have to happen for them to start getting work again.

### 10.

Could frustration in not getting pings add to responders becoming less available?

### 11.

Are there any changes to the code that you would suggest to fix the issue?
