# Changelog

All notable changes to the Clarify plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.0] - 2026-10-30

### Added

- OpenAI ChatGPT plugin directory manifest (`extensions.com.openai` in root plugin.json)
- OpenAI interface configuration with display name, descriptions, capabilities, and starter prompts
- Review test cases: 5 positive scenarios (daily brief, meeting prep, pipeline review, record updates, Lead Finder prospecting) and 3 negative scenarios (unauthorized send, unsupported payments, cross-workspace access)
- Publication metadata for OpenAI directory (US availability, release notes)
- Onboarding skill reference pointing to clarify-setup

### Changed

- Version bumped to 2.1.0 across all plugin manifests (root, Claude, Cursor) to supersede the existing ChatGPT listing (v2.0.0)
- OpenAI category changed to "Business & Operations" to match live listing
- OpenAI longDescription updated to match live ChatGPT listing text with added skills paragraph

## [1.2.0] - 2026-10-26

### Added

- Icon field in Claude manifest for Anthropic directory listing
- Privacy policy URL in Claude manifest (https://www.clarify.ai/privacy)
- Email disclosure in README (connector sends email only after user confirmation)

### Changed

- MCP transport type split: root `mcp.json` uses `streamable-http` for Agent Plugins schema compliance, Claude manifest uses inline `http` config for Anthropic directory
- README positioning from "AI-native CRM" to "full-stack CRM"

## [1.1.0] - 2026-10-16

### Added

- 9 GTM skills: `clarify-setup`, `daily-brief`, `prospect`, `research`, `meeting-prep`, `meeting-followup`, `outreach`, `pipeline-review`, and `clarify-api`
- Shared reference documentation: tool map, workspace profiling, and writing voice guidelines
- Claude Code manifest (.claude-plugin/plugin.json) for http MCP server
- Cursor manifest (.cursor-plugin/plugin.json) with display name and logo
- Marketplace manifest for single-click installation

## [1.0.0] - 2026-09-24

### Added

- Portable Agent Plugin: root `plugin.json` and `mcp.json`, works across Cursor, Claude Code, Cline, Codex, and other compatible clients
- Clarify MCP server pointing at hosted Streamable HTTP endpoint (https://api.clarify.ai/mcp)
- OAuth authentication with Clarify user login (no API key or client id to configure)
- Logo: Clarify official app mark
