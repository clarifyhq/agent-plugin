# MCP tool map

A cheat-sheet from outcome → the Clarify MCP tools that get you there. Tool names and
argument schemas are owned by the hosted server (`tools/list` is the source of truth);
a workspace sees only the tools its enabled features allow. If a tool returns a
"not enabled for this workspace" message, tell the user which Clarify feature to turn on
rather than working around it.

## Reading data

- **query-data** — the primary read tool. Ask in natural language or with structured
  filters ("open deals closing this quarter over $25k", "people at Acme"). Use this before
  reaching for `get-records` when you don't already have IDs.
- **query-analytics** — aggregations and time-series over records (counts, sums, win rate,
  stage movement). Use for "how many", "total", "by stage", "vs last month".
- **get-records** — fetch specific records by id/type when you already know them.
- **get-schema** — entity field definitions and relationships. Call this to learn custom
  fields and objects before filtering or writing.
- **get-current-user** — the signed-in user and workspace context.
- **read-context** — pull additional workspace context when available.

## Finding and importing people/companies

- **find-leads** — Clarify Lead Finder: discover companies/people in the TAM database that
  match an ICP. Returns candidates; nothing is written yet.
- **import-leads** — bring selected Lead Finder results in as records.

## Lists

- **get-lists** / **create-or-update-list** — read and build lists (saved views), static or
  filter-driven. Use lists to define a campaign audience or a working set.

## Campaigns & email

- **create-campaign** / **update-campaign** / **get-campaigns** — campaigns are sequence
  workflows with staggered sending, engagement tracking, and reply detection.
- **get-campaign-recipients** — who's enrolled and where they are in the sequence.
- **create-email-draft** — draft a single email (style-matched) for review before send.
- **send-email** — send an email. Treat as a confirm-before-send action.

## Calendar & meetings

- **get-calendar-events** — upcoming/past events and attendees.
- **create-or-update-calendar-event** / **respond-to-calendar-event** — manage events and RSVPs.
- **get-transcript** — pull a meeting transcript (and highlights) for a recorded meeting.
- **create-meeting-snippet** — turn a transcript moment into a shareable snippet.
- **import-meeting-transcript** — bring in an external transcript.

## Records: writing

- **create-or-update-records** — upsert records (people keyed on email, companies on domain,
  deals on name). The main write tool.
- **merge-records** — combine duplicates.
- **create-or-update-fields** / **create-or-update-object** — extend the schema (custom
  fields and objects). `delete-fields` / `delete-custom-object` to remove.
- **add-comment** — collaborate on a record. **manage-access** — share.

## Artifacts, agents, workflows

- **create-or-update-artifact** — build a report/dashboard/brief as a shareable artifact.
- **create-or-update-agent** / **get-agents** / **get-agent-runs** — Clarify agents.
- **create-or-update-workflow** / **run-workflow** / **get-workflows** / **get-workflow-runs**
  — event-driven automation.

## Attachments & feedback

- **prepare-attachment-upload** → **create-attachment-from-upload** — the two-step file
  upload handshake. Never inline base64 blobs.
- **submit-feedback** — report a problem with the tools.
