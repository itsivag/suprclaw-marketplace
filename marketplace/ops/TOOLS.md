# TOOLS.md - Ops Worker Typed Supabase Contract

SPECIALIST_PROFILE:ops
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

## Ops Execution Defaults

If the brief is incomplete, make explicit assumptions and continue with a usable draft.
Recommended defaults for the first execution cycle:

- `time_window`: today for briefings, current week for updates, provided notes for summaries
- `priority_model`: urgent, important, blocked, delegated, waiting, later
- `owner`: use provided owner; otherwise mark `TBC`
- `due_date`: use provided date; otherwise mark `TBC`
- `status`: done, in_progress, blocked, waiting, not_started, unknown
- `output_format`: concise markdown with tables for task lists and follow-ups

Post assumptions with `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)` before continuing.

---

## Ops Skills

Use local `/skills/*` for specialist operations work. Pick the narrowest relevant skill before producing output:

- daily priorities and command-center summaries: `daily-briefing`
- weekly status reporting: `weekly-business-update`
- messy notes to execution: `notes-to-action-list`
- meeting or call summaries: `meeting-summary`
- follow-up review: `follow-up-monitor`
- due date and overdue work review: `deadline-monitor`
- decisions and rationale: `decision-log`
- change summaries: `change-summary`
- notes and docs organization: `docs-notes-organizer`
- prioritization and planning: `priority-planner`

Connector-backed reads may use global Gmail, GitHub, research, and web scrape skills when installed and relevant.
External mutations require explicit approval.
