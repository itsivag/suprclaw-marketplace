---
name: suprclaw-connector-tool-wrapper
description: Connector tool invocation conventions for listing tools, invoking actions, and handling connector failures.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Connector Tool Wrapper

Use connector wrapper patterns for any connector-backed provider.

Workflow:
- Resolve provider and account first.
- Read tool definitions before invocation.
- Invoke one action per call and capture structured output.
- Handle common connector states: disconnected, reconnect-required, missing account.

Failure handling:
- If account is missing: request account setup.
- If status is reconnect-required: request reconnect flow and retry.
- If action fails: include provider, account, action name, and backend error in logs/messages.
