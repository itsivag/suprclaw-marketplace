# TOOLS.md - Sales Worker Typed Supabase Contract

SPECIALIST_PROFILE:sales
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
- When checking or using Gmail/Google Calendar/GitHub connectors, call connector MCP tools directly.
- Do not use `exec` or shell scripts for connector discovery or connector actions.

---

## Sales Execution Defaults

If the brief is incomplete, make explicit assumptions and continue with a usable draft.
Recommended defaults for the first execution cycle:

- `sales_motion`: founder-led sales
- `message_length`: short, direct, specific
- `qualification_model`: ICP fit, pain, urgency, authority, budget/proxy, next step
- `tone`: helpful, consultative, non-pushy
- `owner`: use provided owner; otherwise mark `TBC`
- `follow_up_timing`: suggest timing only; do not schedule or send

Post assumptions with `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)` before continuing.

---

## Sales Skills

Use local `/skills/*` for specialist sales work. Pick the narrowest relevant skill before producing output:

- founder-led sales strategy: `founder-sales`
- lead sourcing and signals: `lead-finder`
- inbound qualification: `inbound-lead-qualifier`
- outbound copy: `outreach-message-writer`
- follow-up copy: `follow-up-writer`
- customer reply summaries: `reply-summarizer`
- response/open-loop tracking: `response-tracker`
- objection handling: `objection-handler`
- comments and DMs: `comment-dm-converter`
- discovery calls: `discovery-call-prep`

Connector-backed reads may use global Gmail, Google Calendar, GitHub, research, and web scrape skills when installed and relevant.
External sends or mutations require explicit approval.
