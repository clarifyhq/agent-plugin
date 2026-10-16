---
name: meeting-followup
description: Turn what was said on a call into a shareable snippet, a follow-up email draft in your voice, and the CRM updates that keep the deal moving. Use on "write my follow-up", "post-call", "update the CRM from my meeting", "what are the next steps from that call".
metadata:
  author: clarify
  version: '1.0.0'
---

# Meeting follow-up

The after-call workflow, done in one pass: capture the moments that matter, draft the
follow-up, and log the outcomes so the CRM reflects what actually happened. Clarify has the
transcript, so the follow-up and the updates come from what was really said, not memory.

## When to use

- "Write my follow-up from the Acme call."
- "Update the CRM from that meeting."
- "What are the next steps, and send a recap."

## Before you start

Reuse this session's workspace profile (run **clarify-setup** if needed) so you update the
right stage/fields.

## Steps

1. **Get the transcript.** **get-transcript** for the meeting (confirm which one if
   ambiguous). If that tool isn't available in the workspace, read the transcript through
   **query-data** over the meeting (the `meeting`/`meeting_recording` data) instead.
2. **Pull the signal.** Identify decisions, commitments (both sides), objections, next steps,
   and dates. These drive everything below.
3. **Snippet the moments (if available).** For the highlights worth sharing, use
   **create-meeting-snippet** so the team can see the exact exchange. Skip this if the
   workspace doesn't expose snippets.
4. **Draft the follow-up.** **create-email-draft**: a short recap in the sender's voice
   (match the sender, not Clarify's brand voice; keep it short and grounded in what was
   actually said): thank them, confirm what was agreed, restate next steps and owners, one
   clear ask. Leave it as a draft for the user to review. [writing-in-voice](../../references/writing-in-voice.md) covers
   prospect-facing copy.
5. **Update the CRM.** **create-or-update-records** to reflect reality: advance the deal
   stage, update close date/amount if they changed, log the next step, add new contacts met.
   Use **add-comment** for context that doesn't belong in a field.
6. **Confirm before anything leaves.** Show the draft and the proposed updates; apply/send
   only on the user's go-ahead.

## Output

- A recap of what was said (decisions, commitments, next steps, dates).
- The snippet(s) created.
- The follow-up draft, ready to review.
- The CRM changes you propose (or made, once confirmed), stated plainly.

## Notes

- Writes to the workspace, so always confirm the email and the record updates first.
- `send-email` and advancing a deal are confirm-before-act. Drafting and summarizing are safe.
- If you can't get a transcript, ask the user for notes and run the same follow-up from those.
