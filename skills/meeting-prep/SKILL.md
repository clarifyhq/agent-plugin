---
name: meeting-prep
description: A tight pre-call brief for your next meeting: who's attending, their open deals, recent touchpoints, and what was said last time. Use on "prep me for my next call", "what's my next meeting", "brief me before <meeting>", "who am I meeting with".
metadata:
  author: clarify
  version: "1.0.0"
---

# Meeting prep

A 60-second brief for one upcoming call, gaps included. The point is to walk in knowing who
you're talking to, where the deal stands, and what you promised last time, grounded in
Clarify's record of the relationship and past transcripts.

## When to use

- "Prep me for my next call."
- "Brief me before the Acme meeting at 2."
- "Who am I meeting with today and what do I need to know?"

## Before you start

Reuse this session's workspace profile (run **clarify-setup** if needed).

## Steps

1. **Find the meeting.** **get-calendar-events** for the relevant window; pick the meeting
   and read off the attendees (internal vs external).
2. **Match to the CRM.** **query-data** / **get-records** to resolve each external attendee
   to a person and their company.
3. **Deal context.** Pull the open deal(s) tied to the account: stage, amount, close date,
   owner, and recent movement.
4. **Last touchpoints.** Recent activity and emails with these people.
5. **What was said.** If you've met before, pull the highlights from the last call:
   **get-transcript** on that meeting, or **query-data** over the meeting if that tool isn't
   available: commitments, open questions, objections, next steps you agreed to.

## Output

Write it in Clarify's voice: [writing-in-voice](../../references/writing-in-voice.md).

A brief you can read in the hallway:

- **Who**: each external attendee, role, and one useful human detail.
- **Where the deal stands**: stage, amount, close date, and what moved recently.
- **Last time**: the 2–3 things said last call that matter today, including anything you promised.
- **Gaps**: what you don't know and should ask (missing contact, unclear next step, stale info).
- **Your goal**: the one outcome to aim for in this call.

## Notes

- Read-only. If there's no matching CRM record, say so and brief on what the calendar/email shows.
- If meeting recording/transcripts aren't enabled, brief on records + activity and note the gap.
