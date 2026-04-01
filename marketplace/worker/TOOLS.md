# TOOLS.md - Worker SQL Contract

Use Supabase MCP `execute_sql` for mission-control coordination.

## Required RPC-First Contract

Use RPCs for task lifecycle and communication:

```sql
select * from agent_get_my_notifications('<agent_id>');
select agent_ack_notifications('<agent_id>');
select * from agent_get_my_tasks('<agent_id>');
select agent_get_task_context('<task_id>');
select agent_transition_task('<task_id>', 'assigned', 'in_progress', '<agent_id>', 'picked up from webhook');
select agent_post_message('<task_id>', '<agent_id>', '<content>', '<idempotency_key>');
select agent_post_message('<task_id>', '<agent_id>', 'NEEDS_INPUT_FOR_LEAD: missing=<fields>; attempted=<steps>; question=<exact_question>; unblock_condition=<needed_input>', '<idempotency_key>');
select agent_log_action('<agent_id>', '<task_id>', '<action>', '<meta_json>', '<idempotency_key>');
select agent_create_document('<task_id>', '<agent_id>', '<title>', '<content>');
select agent_transition_task('<task_id>', 'in_progress', 'review', '<agent_id>', 'deliverable complete');
select agent_transition_task('<task_id>', 'in_progress', 'blocked', '<agent_id>', '<reason>');
select agent_update_status('<agent_id>', 'active');
```

Assignment wake payloads may be legacy text (`Task <uuid> has been assigned to you`) or structured (`TASK_ASSIGNMENT:`).
In both cases, use the same RPC-first pickup sequence immediately.

`agent_create_document` signature is strict and must be exactly 4 args:
`select agent_create_document('<task_id>', '<agent_id>', '<title>', '<content>');`
Never pass MIME/type/path/URL as extra arguments.
If you see `function agent_create_document(... unknown, unknown, unknown, unknown, unknown) does not exist`,
retry once with the exact 4-arg signature, then mark task `blocked` if it still fails.

Forbidden:
- raw `INSERT/UPDATE/DELETE` on `tasks`, `task_messages`, `task_assignees`, `agent_actions`
- guessed columns/tables (for example `assigned_to`, `metadata`, `messages`)

Identity safety:
- resolve your own `agent_id`
- never hardcode UUIDs
- never copy another agent identity into `from_agent`
- never pass placeholder strings like `'self'` to UUID RPC arguments; use a real UUID

Use skill-specific tooling from `/skills/*` for domain work; keep coordination writes via the SQL contract above.

If missing task details prevent execution, request clarification through `agent_post_message` (this writes to `task_messages`) using the prefix `NEEDS_INPUT_FOR_LEAD:` and then move task to `blocked` with reason `needs input from lead`.
