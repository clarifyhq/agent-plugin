---
name: research
description: A deep brief on an account or person before you reach out — firmographics, open deals, relationship history, and highlights from past calls — saved as a shareable artifact. Use on "research <company/person>", "brief me on <account>", "what do we know about X", "prep a one-pager".
author: clarify
version: 1.0.0
---

# Research

Build a genuinely useful brief on a company or person: not just what's on the record, but
the full relationship — open deals, who knows whom, what was said on past calls, and what's
changed recently. Clarify can pull all of that from one place, so the brief is grounded in
real history, not a web guess.

## When to use

- "Research Acme before my call."
- "What do we know about this person / this account?"
- "Give me a one-pager on <company>."

## Before you start

Reuse this session's workspace profile (run **clarify-setup** if you don't have one) so you
know the custom fields and relationships worth pulling.

## Steps

1. **Find the record.** **query-data** to locate the company/person (by name, domain, or
   email); **get-records** for the full detail once you have it.
2. **The relationship.** Pull connected records — open and past deals, the people at the
   account and their roles, owners, and recent activity. Use the schema's relationships so
   you follow the real graph.
3. **What was said.** If there are past meetings, pull the highlights — **get-transcript**
   for the most recent ones, or **query-data** over those meetings if that tool isn't
   available — commitments, objections, who champions you.
4. **What's changed.** Surface recent signals and updates (new deal detected, stage moved,
   fresh activity) so the brief is current.
5. **(Optional) Save it.** With **create-or-update-artifact**, write the brief as a
   shareable artifact the user can send to the team.

## Output

A one-page brief, skimmable top to bottom:

- **Snapshot** — who they are, size/industry/region, and your current status with them.
- **Deals** — open deals (stage, amount, close date) and relevant past ones.
- **People** — key contacts, roles, and who owns the relationship; flag the champion.
- **History** — the 3–5 things that actually matter from past calls and activity.
- **Angle** — the sharpest reason to reach out now, grounded in a real signal.

## Notes

- Read-only unless the user asks you to save the artifact.
- Prefer facts from the CRM over outside assumptions; if you add external context, label it.
