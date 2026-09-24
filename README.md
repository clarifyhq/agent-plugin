# Clarify

A portable [Agent Plugin](https://agent-plugins.org) that connects AI agents to [Clarify](https://clarify.ai), the AI-native CRM, through Clarify's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Search, create, and update CRM records (people, companies, deals, and custom objects), work with lists, campaigns, and email, manage calendar events and meeting transcripts, and run agents and workflows in the signed-in Clarify workspace.

Because it follows the Agent Plugins standard, it works in any compatible client — Cursor, Claude Code, Cline, Codex, and others.

## Install

This is a standard Agent Plugin, so any compatible client can install it. The universal way is to add the Clarify MCP server to the client's MCP config:

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

On first connect the client opens a Clarify sign-in (OAuth) — there is no API key or client id to configure.

Client-specific shortcuts:

- **Cursor** — Settings → Plugins, search **Clarify**, Install (or `/add-plugin clarify`).
- **Claude Code** — add the block above to your `.mcp.json`, or run `claude mcp add --transport http clarify https://api.clarify.ai/mcp`.
- **Cline, Codex, and other Agent Plugins clients** — point the client at this repository, or add the server block above to the client's MCP config.

## Before you connect

You need a Clarify account with access to a workspace. Tools run as the signed-in user and cannot exceed that user's permissions.

## What agents can do

| Category | Capabilities |
| --- | --- |
| Records & objects | Search, create, update, merge, and delete records; read and edit schema, fields, and custom objects |
| Lists | Inspect, create, update, and delete lists |
| Lead Finder | Find leads and import them as records |
| Campaigns & email | Create and manage campaigns, view recipients, draft and send email |
| Calendar & meetings | Read and manage calendar events, respond to invites, pull transcripts, and create meeting snippets |
| Agents & workflows | Create, run, and inspect agents and workflows |
| Artifacts | Create and manage artifacts such as reports and dashboards |
| Analytics | Query records and run analytics |
| Attachments | Upload file attachments to records |
| Records collaboration | Add comments and manage record access |

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
