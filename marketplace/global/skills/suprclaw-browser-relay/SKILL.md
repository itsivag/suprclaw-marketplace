---
name: suprclaw-browser-relay
description: Browser relay workflow for delegated browser execution through relay MCP sessions.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.1.0"
---

# SuprClaw Browser Relay

Use browser relay tools when the task requires delegated execution through a relay session rather than direct browser control.

Workflow:
- Establish the relay session and confirm at least one relay target is attached.
- Use Agent Browser tools only: `agent_browser_targets_list`, `agent_browser_action`, `agent_browser_batch`.
- Follow strict ref-first flow:
  - take one compact snapshot first (`action=snapshot`, default compact mode),
  - use only `@eN` refs for `click` and `type`,
  - re-snapshot only after a DOM-changing action (navigate/click/type/press).
- Prefer `agent_browser_batch` for multi-step sequences to preserve strict ordering.
- Do not blindly retry when `retry_class` is `never`.
- Request takeover for MFA, CAPTCHA, payment, or destructive actions.
- Resume relay execution and close relay resources when complete.

Use standard cloud/mobile browser tools when relay-specific indirection is not required.
