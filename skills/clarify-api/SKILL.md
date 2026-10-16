---
name: clarify-api
description: Call Clarify's public REST API directly — authentication, JSON:API structure, pagination, filtering, and CRUD on records — for when you need to go beyond the agent tools. Use on "call the Clarify API", "fetch records via API", "create a record with the API", or any direct REST interaction.
author: clarify
version: 1.1.0
---

# Clarify API

Most day-to-day work should go through the Clarify MCP tools (they handle auth and run as
you). Reach for the REST API when you need something scriptable or outside the tool catalog —
a bulk export, a custom integration, a one-off query.

> The Clarify API is under active development and subject to change. Questions: support@clarify.ai

## Root URL

```
https://api.clarify.ai/v1/workspaces/{slug}/*
```

`{slug}` is your workspace ID — find it in the app URL, or under your avatar. The full
OpenAPI spec is at `https://api.clarify.ai/swagger-json` (fetch it for the latest reference
if an endpoint isn't listed below).

## Authentication

### API key (simplest)

Create a key in **Settings → API Keys**. Keys have admin-level access to the workspace
(read/write/delete records; redacted email metadata only; same meeting-data visibility as
other users). Send it as an `api-key` scheme — never log or echo it:

```bash
curl -s -H "Authorization: api-key <key>" \
  https://api.clarify.ai/v1/workspaces/<slug>/schemas | jq .
```

### OAuth 2.0 (for partner apps)

Supports Authorization Code, PKCE, and Refresh Token grants.

- Authorize: `https://auth1.clarify.ai/oauth2/authorize`
- Token / refresh: `https://auth1.clarify.ai/oauth2/token`
- Scopes: `openid profile email offline_access`

Exchange the code for tokens, then call the API with `Authorization: Bearer <access-token>`.

## Structure

The API follows [JSON:API](https://jsonapi.org/).

- **Pagination** — max 1000 items. Request `page[limit]`, `page[offset]`; response carries
  `meta` (`total_records`, `total_pages`, `offset`, `limit`) and `links` (`prev`/`next`).
- **Ordering** — `sortOrder[column]=<field>&sortOrder[dir]=ASC|DESC`.
- **Filtering** — `filter[<field>]=<value>` or `filter[<field>][<operator>]=<value>`.
  Conditions are AND-ed (no OR). Operators depend on field type (text: `Contains`,
  `Starts with`, …; number/date: `Greater than`, `Is before`, …; select: `One of`; etc.).

> **curl tip:** query keys contain `[` and `]`, which curl treats as globs. Pass `-g`
> (`--globoff`) and quote the URL so it's sent literally.

## Endpoints

| Method                | Path                                                   | Description                                                                                     |
| --------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| GET                   | `/schemas`                                             | List all entity schemas (`core/*`, `entities/*`: company, deal, meeting, person, task, user, …) |
| PATCH                 | `/schemas`                                             | Update schema properties                                                                        |
| POST                  | `/schemas/{entity}/properties`                         | Add schema properties                                                                           |
| POST / DELETE         | `/schemas/{entity}/relationships[/{field}]`            | Create / delete schema relationships                                                            |
| GET                   | `/objects/{object}/resources`                          | List records (paginated, filterable, `include`)                                                 |
| GET                   | `/objects/{object}/resources/{id}`                     | Get one resource                                                                                |
| GET / PATCH / DELETE  | `/objects/{object}/records/{id}`                       | Get / update / delete a record                                                                  |
| POST                  | `/objects/{object}/records`                            | Create a record                                                                                 |
| POST                  | `/objects/{object}/records/bulk`                       | Create many records (upsert)                                                                    |
| GET / PATCH / DELETE  | `/objects/{object}/records/{id}/relationships/{field}` | List / set / unset relationships                                                                |
| GET                   | `/objects/{object}/records/{id}/activities`            | List a record's activities                                                                      |
| POST / PATCH / DELETE | `/comments[/{id}]`                                     | Create / update / delete a comment                                                              |
| POST                  | `/objects/{object}/lists/{list}/rows/csv`              | Export list rows as CSV                                                                         |
| POST                  | `/meetings/{meetingId}/recordings/{id}/artifacts`      | Get recording video + transcript URLs                                                           |
| POST                  | `/meetings/{meetingId}/transcript`                     | Upload a meeting transcript                                                                     |

**Upsert keys** (for `records/bulk`): person → any `email_addresses`; company → any
`domains`; deal → `name`. Meetings/recordings/users have none. There is no bulk delete today.

## Request shapes

**Create / update** use the JSON:API envelope:

```bash
curl -s -X POST 'https://api.clarify.ai/v1/workspaces/<slug>/objects/person/records' \
  -H "Authorization: api-key <key>" -H "Content-Type: application/json" \
  -d '{"data":{"type":"person","attributes":{"name":{"first_name":"Jane","last_name":"Doe"},"email_addresses":{"items":["jane@acme.com"]}}}}' | jq .
```

> Some fields are structured objects, not plain scalars: `person.name` is
> `{ first_name, last_name, ... }` and `email_addresses` is a collection, `{ items: [...] }`.
> Check `/schemas` (or `GET /schemas` above) for the exact shape of any field before writing.

```bash
curl -s -g -X PATCH 'https://api.clarify.ai/v1/workspaces/<slug>/objects/deal/records/<id>' \
  -H "Authorization: api-key <key>" -H "Content-Type: application/json" \
  -d '{"data":{"id":"<id>","type":"deal","attributes":{"stage":"Won"}}}' | jq .
```

> `stage` is a restricted enum. The default deal stages are `Lead`, `In progress`, `Won`,
> `Lost` — so `"Won"` closes a deal as a win. A workspace with a customized pipeline uses its
> own stage values; read them from `/schemas` and use the exact strings defined there.

**Set a relationship:** `PATCH …/records/{id}/relationships/{field}` with
`{"data":[{"id":"<related-id>","type":"<object>"}]}` (use `DELETE` to unset).

## Handling results

- Summarize in plain language ("Created `rec_abc123` — Acme Corp").
- On non-2xx, show the status and the validation errors from the body. Common cases:
  **401** invalid/expired key, **403** key lacks permission, **404** check slug/object/id,
  **422** validation — read the body.
- For big responses, `jq` out the fields that matter instead of dumping everything.
