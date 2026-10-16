---
name: pipeline-review
description: One shareable page on your pipeline — what's moving, what's at risk, and what to do this week — built from your real deal data. Use on "pipeline review", "how's my pipeline", "what's at risk", "forecast", "deal review", "what should I work this week".
author: clarify
version: 1.0.0
---

# Pipeline review

A clear read on the pipeline: where it stands, what's moving, what's slipping, and the
handful of actions that matter this week. Built from the workspace's real deals and
analytics, and optionally saved as a page the user can share with their manager or team.

## When to use

- "How's my pipeline?" / "Pipeline review."
- "What's at risk?" / "What should I work this week?"
- Weekly deal review, or prepping a forecast conversation.

## Before you start

Reuse this session's workspace profile (run **clarify-setup** if needed) so you use the
right stages, amount, close-date, and owner fields. Confirm scope: just the user, or the team.

## Steps

1. **The shape.** **query-analytics** for pipeline by stage, total open value, and how it's
   changed (created, advanced, slipped) over the period.
2. **What's moving.** **query-data** for deals that advanced or were newly detected — the
   momentum story.
3. **What's at risk.** Deals that are stalled (no activity in N days), past close date, or
   stuck in a late stage too long. This is the part people actually act on.
4. **This week.** From the above, pick the specific deals that need a push and what the push
   is (a nudge, a prep, a stakeholder to loop in).
5. **(Optional) Make it shareable.** **create-or-update-artifact** to write the review as a
   page/report the user can send on.

## Output

One skimmable page:

- **Headline** — open pipeline value, # of deals, and the net change this period.
- **By stage** — where value sits, with anything unusual called out.
- **Moving** — the deals with momentum.
- **At risk** — stalled/slipping deals, newest problems first, each with the reason.
- **Do this week** — a short, specific action list tied to named deals.

Lead with the one thing that matters most; don't bury it under a table.

## Notes

- Read-only unless the user asks you to save the artifact.
- If a stage or field is ambiguous, confirm once (via `clarify-setup`) rather than guessing.
- Offer the obvious follow-ons: `outreach` for a stalled segment, `meeting-prep` for a key call.
