---
name: github-connector
description: Use when the user asks to read or mutate GitHub resources via their connected GitHub account in SuprClaw. This skill must use the connector wrapper APIs, not direct GitHub APIs.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# GitHub Connector

Use the authenticated GitHub connector through SuprClaw backend wrapper routes.

Do not:
- call GitHub REST/GraphQL directly
- call connector backend APIs directly without the wrapper contract
- assume any action name exists without discovery

## Preconditions

1. A GitHub connector account is connected for the user.
2. Runtime can call SuprClaw backend APIs.

If either precondition fails, stop and explain what is missing.

## Endpoint Rules

- Backend base URL must be `${WEBHOOK_BASE_URL}` when available, otherwise `https://api.suprclaw.com`.
- Never assume `localhost`, `127.0.0.1`, or port `3000` for connector wrapper routes.
- Prefer runtime-scoped routes from agent runtime sessions:
  - `GET ${baseUrl}/api/runtime/connectors/github/accounts`
  - `GET ${baseUrl}/api/runtime/connectors/github/accounts/{accountId}/tools`
  - `POST ${baseUrl}/api/runtime/connectors/github/accounts/{accountId}/tools/{toolName}/invoke`
- Runtime-scoped route auth headers:
  - `Authorization: Bearer ${SUPRCLAW_TOOLS_CRON_WEBHOOK_SECRET}`
  - `X-Suprclaw-Project-Ref: ${SUPABASE_PROJECT_REF}`
- Runtime auth must come directly from env vars above.
- If either runtime auth env var is missing, stop and report missing runtime auth.
- Do not execute placeholder auth headers (for example `Bearer ${...}` with empty values). Ask for valid auth first.

## Workflow

1. List GitHub accounts:

```http
GET /api/runtime/connectors/github/accounts
```

2. Select account in this order:
- user-requested account
- agent-specific default
- provider default
- otherwise ask

3. Discover available GitHub actions for that account:

```http
GET /api/runtime/connectors/github/accounts/{accountId}/tools
```

4. Invoke the chosen action:

```http
POST /api/runtime/connectors/github/accounts/{accountId}/tools/{toolName}/invoke
Content-Type: application/json

{
  "input": {},
  "async": false
}
```

## Guardrails

- For write operations (create/update/delete), summarize intended mutation and target repo/branch before invoking.
- Prefer read-only actions first when user intent is ambiguous.
- Always surface connector/tool errors verbatim and suggest the next recovery step.

## Output Format

Report:
1. account used
2. tool invoked
3. read-only vs mutating
4. key result artifacts (URLs, IDs, commit SHAs, PR numbers)
