---
name: clarify-setup
description: Learn how a Clarify workspace actually sells (pipeline stages, ICP, custom objects, and fields) and cache it so other skills fit this setup. Run this first. Use when connecting to a new workspace, or on "set up Clarify", "learn my CRM", "how is my pipeline configured".
metadata:
  author: clarify
  version: '1.0.0'
---

# Clarify setup

Every Clarify workspace is shaped differently. Before you prospect, research, or review a
pipeline, learn how _this_ workspace sells so the other skills speak its language. Run this
once at the start of a session; keep what you learn for the rest of it.

## When to use

- The first time you connect to a workspace in a session.
- When the user asks you to "set up", "learn my CRM", or "figure out how my pipeline works".
- Whenever a later skill hits something ambiguous (two "stage"-like fields, an unknown custom object).

## Steps

1. **get-current-user**: confirm the signed-in user and workspace.
2. **get-schema** for `person`, `company`, `deal`, and any custom objects. Capture deal
   stages (in order), the amount / close-date / owner fields, the fields that define ICP,
   and any custom fields that matter.
3. **get-lists**: see the saved views the team actually uses; these reveal real segments.
4. **query-analytics** / **query-data**: spot-check with live data ("deals by stage",
   "companies by industry") so you record the values that are _in use_, not just defined.

## Output

Write it in Clarify's voice: [writing-in-voice](../../references/writing-in-voice.md).

Give the user a short, friendly profile of their workspace and confirm it:

- Pipeline: the stages in order, and which are open / won / lost.
- Deal fields: amount, close date, owner.
- ICP: the fields and typical values that describe their best-fit customers.
- Custom objects/fields worth knowing about.
- The lists they lean on.

End by confirming anything ambiguous with **one** question, then remember the answer.
Keep this profile in mind so no other skill has to re-derive it.

> Example close: "Here's how your workspace is wired. Pipeline runs Discovery → Eval →
> Proposal → Closed Won/Lost, deals carry Amount and Close Date, and your ICP leans
> mid-market SaaS. One thing: you've got both 'Stage' and 'Status'; which one drives your
> pipeline?"

## Notes

- Read-only. This skill never writes to the workspace.
- If a tool reports a feature isn't enabled, note it and move on. Don't work around it.
