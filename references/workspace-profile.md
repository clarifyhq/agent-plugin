# Workspace profile

Every Clarify workspace sells differently — custom pipeline stages, custom objects, custom
fields, its own ICP. Before filtering, writing, or summarizing, learn the shape of _this_
workspace instead of assuming a fixed CRM model. The `clarify-setup` skill builds this
profile once; other skills reuse it.

## How to build it

1. **Who and where** — call **get-current-user** for the signed-in user and workspace.
2. **Entities and fields** — call **get-schema** for each entity you'll touch (at least
   `person`, `company`, `deal`, plus any custom objects). Capture:
   - deal **stages** and the field that holds them, amount field, close-date field, owner field
   - the fields that encode **ICP** (industry, size, segment, region) on company/person
   - any **custom objects** and custom fields unique to this workspace
3. **Saved views** — call **get-lists** to see how the team already slices their data
   (these reveal the segments and definitions the team actually uses).
4. **Sanity-check with real data** — run a couple of **query-data** / **query-analytics**
   calls ("deals by stage", "companies by industry") to confirm which stages and values are
   actually in use, not just defined.

## What to remember

Hold onto these for the rest of the session so other skills don't re-derive them:

- Deal stage names in pipeline order, and which count as open vs won vs lost
- The amount, close-date, and owner fields
- The ICP-defining fields and their common values
- Custom objects/fields and what they mean
- The lists/views the team relies on

When something is ambiguous (e.g. two fields that could be "stage"), ask the user once and
remember the answer rather than guessing on every call.
