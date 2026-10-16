---
name: daily-brief
description: Your day in Clarify — what moved since yesterday, which meetings matter, which replies need you, and what to do first. Use on "daily brief", "what's on today", "catch me up", "what changed", "start my day".
author: clarify
version: 1.0.0
---

# Daily brief

A 60-second read on the day: what changed, what needs the user, and what to do first.
Built for the morning scan, but works any time someone asks to be caught up.

## When to use

- "What's on today?", "catch me up", "start my day", "what changed since yesterday".

## Before you start

If you haven't already this session, run **clarify-setup** so you know the workspace's
stages, owner field, and ICP. Scope everything to the signed-in user unless they ask for
the team's view.

## Steps

1. **Today's calendar** — **get-calendar-events** for today (and tomorrow morning). Flag
   external meetings and anything tied to an open deal.
2. **What moved** — **query-data** / **query-analytics** for recent changes: deals that
   changed stage, new deals Clarify detected, deals pushed past their close date, records
   created or updated since yesterday.
3. **Who needs a reply** — surface recent inbound/replies and any campaign replies
   (**get-campaigns** / **get-campaign-recipients**) waiting on the user.
4. **Open loops** — tasks, follow-ups, and stalled deals (no activity in N days) that the
   user owns.

## Output

A tight, skimmable brief in the user's voice — not a data dump:

- **First thing** — the single most important action, called out up top.
- **Meetings** — today's calls, who's on them, and which have an open deal; offer
  `meeting-prep` for the important one.
- **Moved** — deals and records that changed, newest first.
- **Needs you** — replies and asks waiting on the user.
- **At risk** — stalled or slipping deals worth a nudge; offer `pipeline-review` for the full picture.

Keep it to what a person can act on before their coffee's cold. Link out, don't transcribe.

## Notes

- Read-only. Suggest next actions (prep, nudge, review) but don't take them without a yes.
- If calendar or email features aren't enabled for the workspace, say so and brief on what you can see.
