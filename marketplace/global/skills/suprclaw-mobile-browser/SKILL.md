---
name: suprclaw-mobile-browser
description: Mobile browser MCP workflow for interactive device-like browsing and task execution.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Mobile Browser

Use mobile browser tools for flows that must be tested or executed in a mobile browsing context.

Workflow:
- Use current chat/session binding (`sessionKey` when required).
- Mandatory interaction loop: `mobile_browser_snapshot` -> choose `ref` (`@eN`) -> action (`click|touch|hover|type|wait_for`) -> resnapshot after navigation or mutating actions.
- `selector` for `click|touch|hover|type|wait_for(selector mode)` must be snapshot refs (`@eN`), optionally with `ref_generation`.
- Treat `SNAPSHOT_REF_NOT_FOUND` as stale refs: resnapshot and retry with fresh refs.
- On `TAKEOVER_REQUIRED`, hand control to the user and resume only after takeover completes.
- Return exact tool errors and codes as-is (`SNAPSHOT_REF_REQUIRED`, `SNAPSHOT_REF_NOT_FOUND`, `ACTIONABILITY_*`, `ACTION_TIMEOUT`, etc.); do not substitute generic fallback explanations.
- Retry only explicitly retryable transport/runtime failures. Do not blind-retry deterministic actionability/ref errors without state change.

Prefer `web_scrape` for read-only extraction and `cloud_browser_*` for desktop-style interaction.
