# TOOLS.md - Research Worker Typed Supabase Contract

SPECIALIST_PROFILE:research
COORDINATION_PROTOCOL:V1

Mission-control task coordination uses typed Supabase MCP tools. Connector operations use connector MCP tools.
Load and obey `skills/suprclaw-supabase/SKILL.md` (`TASK_DB_CONTRACT_V3`) before task coordination work. For connector reads or actions, call connector MCP tools directly and do not use `exec` as a connector fallback.

---

## Worker Tool Surface

- `mcp_supabase_get_notifications(caller_id=<supabase_uuid>)`
- `mcp_supabase_ack_notifications(caller_id=<supabase_uuid>)`
- `mcp_supabase_get_tasks(caller_id=<supabase_uuid>)`
- `mcp_supabase_get_task_context(caller_id=<supabase_uuid>, task_id=<task_uuid>)`
- `mcp_supabase_start_task(caller_id=<supabase_uuid>, task_id=<task_uuid>)`
- `mcp_supabase_post_message(caller_id=<supabase_uuid>, task_id=<task_uuid>, content=<text>, idempotency_key=<key>)`
- `mcp_supabase_request_lead_input(caller_id=<supabase_uuid>, task_id=<task_uuid>, missing=<text>, attempted=<text>, question=<text>, unblock_condition=<text>, idempotency_key=<key>)`
- `mcp_supabase_log_action(caller_id=<supabase_uuid>, task_id=<task_uuid_or_null>, action=<label>, meta=<json_object>, idempotency_key=<key>)`
- `mcp_supabase_create_document(caller_id=<supabase_uuid>, task_id=<task_uuid>, title=<title>, content=<content>, idempotency_key=<key>)`
- `mcp_supabase_submit_task_for_review(caller_id=<supabase_uuid>, task_id=<task_uuid>)`
- `mcp_supabase_block_task(caller_id=<supabase_uuid>, task_id=<task_uuid>, reason=<reason>)`
- `mcp_supabase_set_agent_status(caller_id=<supabase_uuid>, status=<idle|active|blocked|offline>)`

## Connector Tool Surface

- `connector_accounts_list`
- `connector_tools_list`
- `connector_action_invoke`

Connector-first rule:
- When checking or using Gmail/GitHub connectors, call connector MCP tools directly.
- Do not use `exec` or shell scripts for connector discovery or connector actions.

---

## Research Execution Notes

- Read task context before each write
- Post assumptions, findings, source links, and tradeoffs in `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)`
- Save durable output in `mcp_supabase_create_document(caller_id=<supabase_uuid>, ...)`
- Use `mcp_supabase_request_lead_input(caller_id=<supabase_uuid>, ...)` only when the blocker is real and specific

Use local `/skills/*` for research analysis and synthesis. Keep Mission Control coordination in the typed Supabase tools listed above.
