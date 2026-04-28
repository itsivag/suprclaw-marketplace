---
name: suprclaw-gmail-connector
description: Use connector-backed Gmail actions through the SuprClaw connector account workflow.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Gmail Connector

Use this skill when a task needs Gmail actions through connector accounts.

Workflow:
- Ensure a connected Google Mail account exists for the current user.
- List available connector tools for that account.
- Invoke the required connector action with minimal inputs first.
- Validate action output before posting results back to task context.

Rules:
- Prefer connector actions over ad-hoc API key usage.
- Do not assume a single default account; use the account tied to the current workflow.
- If reconnect is required, trigger connector re-auth before retrying actions.
