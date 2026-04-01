---
name: connector-tool-wrapper
description: Use when a task requires operating on a connected third-party account through SuprClaw's connector wrapper instead of calling the provider directly. Trigger for requests like "use my GitHub connection", "run this through the connected account", "list connector tools", "invoke a connector tool", "use the repo integration", or "work through the connected app". Prefer this skill over direct vendor APIs or direct connector backend usage. Current primary provider is GitHub, but the workflow is provider-neutral.
---

# Connector Tool Wrapper

Use SuprClaw's connector wrapper as the execution boundary for connected third-party apps.

Do not:
- call vendor APIs directly
- call the connector backend directly
- start OAuth from the agent
- assume a provider account exists or is connected

## Preconditions

This skill only works if the runtime already has an authenticated way to call the SuprClaw backend.

If backend auth is not available from the runtime, stop and report that the connector wrapper is not reachable from the current agent session.

If no provider account is connected, tell the user to complete connector auth in the client app first.

## Endpoint Rules

- Resolve backend base URL from `${WEBHOOK_BASE_URL}` when present; otherwise use `https://api.suprclaw.com`.
- Never target `localhost`, `127.0.0.1`, or `:3000` for connector wrapper APIs.
- For runtime agent calls, prefer `${baseUrl}/api/runtime/connectors/...` with:
  - `Authorization: Bearer ${SUPRCLAW_TOOLS_CRON_WEBHOOK_SECRET}`
  - `X-Suprclaw-Project-Ref: ${SUPABASE_PROJECT_REF}`
- Runtime auth must come directly from env vars above.
- If either runtime auth env var is missing, stop and report missing runtime auth.
- Do not run placeholder auth commands (for example `Bearer ${...}` without a real token). Ask for auth context first.

## Provider-Neutral Workflow

1. Identify the target provider and task.
2. List connected accounts for that provider:

```http
GET /api/runtime/connectors/{provider}/accounts
```

3. Pick an account using this order:
- explicit account requested by the user
- agent-specific default if known
- provider default
- otherwise ask or stop

4. Discover available tools:

```http
GET /api/runtime/connectors/{provider}/accounts/{accountId}/tools
```

5. Invoke the selected tool through the generic wrapper route:

```http
POST /api/runtime/connectors/{provider}/accounts/{accountId}/tools/{toolName}/invoke
```

Request body:

```json
{
  "input": {},
  "async": false
}
```

## Decision Rules

- Prefer wrapper tools over cloud browser when the requested operation already exists as a connector tool.
- Use cloud browser only when the task needs UI interaction that the connector wrapper does not expose.
- If multiple tools could work, choose the least destructive one first.
- If the tool is write-capable, summarize the planned mutation before invoking it.

## GitHub Examples

Common GitHub use through this wrapper:
- list repositories
- read repository files
- write repository files
- create issues or follow-up tasks

Always discover the actual available tool names from `/tools` first. Do not hardcode assumed action names.

## Output Requirements

When using this skill, report:
- which provider account was used
- which wrapper tool was invoked
- whether the action was read-only or mutating
- any returned artifact URLs, ids, or created resources

If blocked, state exactly which prerequisite is missing:
- no connected account
- no backend auth from runtime
- no matching tool exposed by the wrapper
