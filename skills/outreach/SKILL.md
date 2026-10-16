---
name: outreach
description: Compose a personalized campaign from a list in Clarify — with per-recipient context pulled from the CRM — ready for you to activate, then track it through to replies. Use on "run a campaign", "set up outreach", "email this list", "sequence these leads", "reach out to <segment>".
author: clarify
version: 1.0.0
---

# Outreach

Turn a list of people into a personalized, tracked campaign. In Clarify a campaign is a
sequence workflow — staggered sending, engagement tracking, and reply detection built in —
so this skill is about getting the audience, the message, and the personalization right,
then letting Clarify run it.

## When to use

- "Run a campaign to these leads."
- "Set up outreach for <segment>."
- "Email the list I just built and follow up if they don't reply."

## Before you start

Reuse this session's workspace profile (run **clarify-setup** if needed). If there's no
audience yet, run **prospect** first to build one.

## Steps

1. **Nail the audience.** Use an existing list or build one with **create-or-update-list**
   (or the output of `prospect`). Confirm the count and that these are the right people.
2. **Agree the angle.** With the user, settle the goal, the offer, and the number of steps
   (e.g. intro → value → break-up). Keep it short and specific.
3. **Draft, personalized.** Write each step grounded in real CRM context — recent signals,
   shared connections, what was said on past calls (`research` is great upstream here).
   Match the **sender's** voice (not Clarify's brand voice), factual subject, one clear ask.
   Use **create-email-draft** to show a sample personalized for a real recipient so the user
   can judge the quality before you build the campaign.
4. **Build the campaign as a draft.** **create-campaign** with the audience, steps, and
   timing; **update-campaign** to adjust while it's still a draft. Keep personalization tied
   to CRM fields so each recipient gets their own version, not a mail-merge blank. Note that
   campaigns are created **disabled (draft)** and can only be edited _before_ they're sent.
5. **Hand off activation.** The agent tools can't start a campaign — **create-campaign**
   returns a review-and-activate link. Give the user that link and tell them to activate it
   in Clarify once they're happy with the audience and copy. Don't claim it's been sent.
6. **Track.** **get-campaigns** / **get-campaign-recipients** to report opens, replies, and
   where people are in the sequence; flag replies that need a human and offer `meeting-prep`
   or `meeting-followup` when one converts.

## Output

- The audience (list + count) and the agreed sequence.
- A sample fully-personalized step for a real recipient.
- The draft campaign and its review-and-activate link, with a note that the user activates it
  in Clarify. Once it's live, how to watch replies.

## Notes

- Sending is a real, outward-facing action — but it happens when the **user** activates the
  campaign in Clarify, not from here. Get their sign-off on audience **and** copy, and respect
  their sending limits and compliance norms.
- If campaigns aren't enabled for the workspace, tell the user how to turn them on.
- Personalize from CRM facts; never fabricate a detail to sound personal.
