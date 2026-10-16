---
name: prospect
description: Find accounts and contacts that match your ICP with Clarify's Lead Finder and bring them in, deduped against what you already have. Use on "find leads", "prospect", "build a list of companies like X", "who should we go after", "find people at target accounts".
metadata:
  author: clarify
  version: '1.0.0'
---

# Prospect

Find net-new accounts and contacts that look like the customer's best-fit buyers, then
import the good ones without creating duplicates. This leans on Clarify's **Lead Finder**
and TAM database, so it can discover companies and people that aren't in the CRM yet.

## When to use

- "Find me 50 companies like our best customers."
- "Who are the decision-makers at these target accounts?"
- "Build a prospecting list for <segment>."

## Before you start

Run **clarify-setup** first (or reuse this session's profile) so you know the real ICP
fields and values, and which lists the team uses. If the ICP is still fuzzy, ask the user
to name 2–3 existing customers you can treat as the pattern.

## Steps

1. **Define the target.** Translate the ICP into Lead Finder criteria (industry, size,
   region, role/seniority, signals). Confirm the shape with the user in one line before
   searching.
2. **Find.** Call **find-leads** with those criteria. This returns candidates from the TAM
   database. Nothing is written yet. Show a sample and the count.
3. **Refine until the search _is_ the list.** Import works off the saved search, not a
   hand-picked subset. It brings in the top N rows (by your `count`, or all of them).
   So you can't cherry-pick individual preview rows; instead tighten or loosen the criteria
   until the search itself contains the people you want. Narrow beats noisy: better to
   import 30 great fits than 300 maybes.
4. **Check for overlap.** With **query-data**, see how much of the search is already in the
   CRM (people by email, companies by domain). Import automatically skips records that
   already exist, but knowing the overlap tells you how many _new_ records you'll actually get.
5. **Import.** With the user's go-ahead, **import-leads** on the refined search, with a
   `count` if you only want the top N. It imports from the top of the search and skips
   existing records. Optionally group the results into a list with **create-or-update-list**
   so they're ready for `research` or `outreach`.

## Output

- A short summary of the criteria used and how many fit.
- The sample you reviewed, with overlaps flagged.
- After import: how many records came in, how many were already known, and the list they
  landed in, plus the obvious next step ("want me to research the top 10, or line up outreach?").

## Notes

- `find-leads` is read-only discovery; `import-leads` writes records and can consume credits.
  Always confirm the refined search and count before importing, since import pulls the top N
  of the search rather than a subset you picked by hand.
- If Lead Finder isn't enabled for the workspace, tell the user how to turn it on rather
  than scraping elsewhere.
- Respect sending/compliance norms. Importing a lead isn't permission to spam it.
