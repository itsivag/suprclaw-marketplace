# TOOLS.md - SEO Worker Typed Supabase Contract

SPECIALIST_PROFILE:seo
COORDINATION_PROTOCOL:V1

Mission-control coordination uses typed Supabase MCP tools only.
Load and obey `skills/suprclaw-supabase/SKILL.md` (`TASK_DB_CONTRACT_V3`) before coordination work.

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

---

## SEO Execution Notes

- Read task context before each write
- Post assumptions, findings, and tradeoffs in `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)`
- Save durable output in `mcp_supabase_create_document(caller_id=<supabase_uuid>, ...)`
- Use `mcp_supabase_request_lead_input(caller_id=<supabase_uuid>, ...)` only when the blocker is real and specific

Use local `/skills/*` for SEO-specific analysis. Keep Mission Control coordination in the typed Supabase tools listed above.
