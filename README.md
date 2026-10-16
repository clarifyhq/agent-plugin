# Clarify

A portable [Agent Plugin](https://agent-plugins.org) that connects AI agents to [Clarify](https://clarify.ai), the AI-native CRM, through Clarify's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server — and teaches them the plays your GTM team runs every day.

Search, create, and update CRM records (people, companies, deals, and custom objects), work with lists, campaigns, and email, manage calendar events and meeting transcripts, and run agents and workflows in the signed-in Clarify workspace. The bundled **skills** turn those raw tools into end-to-end workflows: prospect, research, prep for a call, follow up, run outreach, and review your pipeline.

Because it follows the Agent Plugins standard, it works in any compatible client — Cursor, Claude Code, Cline, Codex, and others.

## Install

This repo is a complete Agent Plugin — the Clarify MCP **connection** and the **skills**
in `skills/`. Install it as a _plugin_ (not just the MCP server) so your client picks up
both; a compatible client discovers the skills from the repo automatically.

- **Cursor** — Settings → Plugins, search **Clarify**, Install (or point Cursor at this
  repository). You'll get the connector and the skills.
- **Claude Code** — install this repository as a plugin (e.g. via `/plugin`) so the skills
  come along, then sign in on first connect.
- **Cline, Codex, and other Agent Plugins clients** — point the client at this repository;
  it loads the connector and the bundled skills.

On first connect the client opens a Clarify sign-in (OAuth) — there is no API key or client
id to configure.

### Connector only (tools, without the skills)

If you only want the CRM tools and not the skill playbooks, add the MCP server to the
client's config directly:

```json
{
  "mcpServers": {
    "clarify": {
      "type": "streamable-http",
      "url": "https://api.clarify.ai/mcp"
    }
  }
}
```

This registers the CRM tools but **not** the skill playbooks — install the plugin (above)
to get those. In Claude Code you can also add the connector with
`claude mcp add --transport http clarify https://api.clarify.ai/mcp`.

## Before you connect

You need a Clarify account with access to a workspace. Tools run as the signed-in user and cannot exceed that user's permissions.

## Skills

Skills are short playbooks that tell the agent how to chain Clarify's tools into a real GTM workflow. Compatible clients discover them automatically — just ask for the outcome ("prep me for my next call", "find 50 leads like our best customers", "what's at risk in my pipeline this week") and the matching skill kicks in.

Run `clarify-setup` first — it learns how your workspace actually sells (stages, ICP, custom objects) so every other skill speaks your CRM's language.

| Skill                | What it does                                                                                                                                                            |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **clarify-setup**    | Learns how your workspace sells — pipeline stages, ICP, custom objects and fields — and caches it so the other skills fit your setup. Run this first.                   |
| **daily-brief**      | Your day in 60 seconds: what moved since yesterday, which meetings matter, which replies need you, what to do first.                                                    |
| **prospect**         | Finds accounts and contacts that match your ICP with Clarify's Lead Finder and brings them in — deduped against what you already have.                                  |
| **research**         | A deep brief on an account or person before you reach out: firmographics, open deals, relationship history, and highlights from past calls.                             |
| **meeting-prep**     | A tight pre-call brief for your next meeting — who's attending, open deals, recent touchpoints, and what was said last time.                                            |
| **meeting-followup** | Turns what was said on a call into a shareable snippet, a follow-up draft in your voice, and the CRM updates that keep the deal moving.                                 |
| **outreach**         | Composes a personalized campaign from a list, with per-recipient context pulled from the CRM, ready for you to activate in Clarify — then tracks it through to replies. |
| **pipeline-review**  | One shareable page: what's moving, what's at risk, and what to do this week — built from your real deal data.                                                           |
| **clarify-api**      | A reference for calling Clarify's public REST API directly (auth, filtering, CRUD) when you need to go beyond the agent tools.                                          |

More on the way: **crm-hygiene** (dedupe, merge, and fill the gaps) and **automate** (turn a recurring play into a Clarify agent or workflow).

The [`references/`](references/) folder holds shared background the skills draw on — a tool map, how to profile a workspace, and Clarify's writing voice.

## What agents can do

| Category              | Capabilities                                                                                        |
| --------------------- | --------------------------------------------------------------------------------------------------- |
| Records & objects     | Search, create, update, merge, and delete records; read and edit schema, fields, and custom objects |
| Lists                 | Inspect, create, update, and delete lists                                                           |
| Lead Finder           | Find leads and import them as records                                                               |
| Campaigns & email     | Create and manage campaigns, view recipients, draft and send email                                  |
| Calendar & meetings   | Read and manage calendar events, respond to invites, pull transcripts, and create meeting snippets  |
| Agents & workflows    | Create, run, and inspect agents and workflows                                                       |
| Artifacts             | Create and manage artifacts such as reports and dashboards                                          |
| Analytics             | Query records and run analytics                                                                     |
| Attachments           | Upload file attachments to records                                                                  |
| Records collaboration | Add comments and manage record access                                                               |

The hosted runtime is the source of truth for tool names and schemas. A workspace sees a filtered view of the catalog based on its enabled features.

## Notes

- Tool calls run as the Clarify user who authorizes the connection and cannot exceed that user's permissions.
- Read operations are auto-approved. Write operations request confirmation before they change workspace data.
- Clarify hosts the server itself; this plugin does not wrap a local stdio server.
- Revoke access at any time from your Clarify account settings.

## Docs

- Connect an AI agent to Clarify: https://developer.clarify.ai/docs/getting-started/ai-agents
- Authentication: https://developer.clarify.ai/docs/getting-started/authentication
- Server URL: https://api.clarify.ai/mcp

## License

MIT
