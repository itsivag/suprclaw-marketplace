# HEARTBEAT.md — Worker Execution Protocol

SPECIALIST_PROFILE:content-writer
COORDINATION_PROTOCOL:V1

Run in order. Every heartbeat.
Typed Supabase MCP state is the source of truth.
Follow `skills/suprclaw-supabase/SKILL.md` (`TASK_DB_CONTRACT_V3`) for the canonical typed tool contract.

---

## Pre-Flight

- Capture timestamp and cycle number for idempotency keys

---

## 1 — Notifications

1. Call `mcp_supabase_get_notifications(caller_id=<supabase_uuid>)`
2. Call `mcp_supabase_ack_notifications(caller_id=<supabase_uuid>)`
3. For any referenced task, call `mcp_supabase_get_task_context(caller_id=<supabase_uuid>, task_id=<task_uuid>)`

Notifications tell you where to look. Task context tells you what to do.

---

## 2 — Queue

Call `mcp_supabase_get_tasks(caller_id=<supabase_uuid>)`.
Only work on tasks assigned to you.

---

## 3 — Process Each Task

For each assigned task:

1. Call `mcp_supabase_get_task_context(caller_id=<supabase_uuid>, task_id=<task_uuid>)`
2. If the task is still `assigned`, call `mcp_supabase_start_task(caller_id=<supabase_uuid>, task_id=<task_uuid>)`
3. Do one meaningful step of work
4. Post progress with `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)`
5. Log the step with `mcp_supabase_log_action(caller_id=<supabase_uuid>, ...)`
6. Save output with `mcp_supabase_create_document(caller_id=<supabase_uuid>, ...)` when you produced a deliverable
7. If complete, call `mcp_supabase_submit_task_for_review(caller_id=<supabase_uuid>, task_id=<task_uuid>)`

---

## 4 — Blockers

If you are genuinely blocked:

1. Call `mcp_supabase_request_lead_input(caller_id=<supabase_uuid>, ...)`
2. Call `mcp_supabase_log_action(caller_id=<supabase_uuid>, ...)` with `action=task_blocked`
3. Call `mcp_supabase_block_task(caller_id=<supabase_uuid>, task_id=<task_uuid>, reason=<reason>)`

Never wait silently.

---

## 5 — Presence

- If you worked this cycle, call `mcp_supabase_set_agent_status(caller_id=<supabase_uuid>, status=active)`
- If no work was required, call `mcp_supabase_set_agent_status(caller_id=<supabase_uuid>, status=idle)`

---

## Final Step

Return `HEARTBEAT_OK` only when there were no actionable notifications, no assigned tasks, and no new progress.
