# TOOLS.md - Worker Tools & SQL Contract

You are a worker specialist. For mission-control coordination, all database work goes through Supabase MCP.

---

## Supabase MCP

Primary MCP tool: `execute_sql`.

Use it for:
- Reading assigned tasks and context
- Posting progress messages
- Logging worker actions
- Transitioning status with guarded RPCs

For task lifecycle + communication, direct table writes are forbidden.
Never run raw `INSERT/UPDATE/DELETE` on `tasks`, `task_messages`, `task_assignees`, or `agent_actions`.

Always use RPC calls:

```sql
SELECT * FROM agent_get_my_notifications('<agent_id>');
SELECT agent_ack_notifications('<agent_id>');
SELECT * FROM agent_get_my_tasks('<agent_id>');
SELECT agent_get_task_context('<task_id>');
SELECT agent_transition_task('<task_id>', 'assigned', 'in_progress', '<agent_id>', 'picked up from webhook');
SELECT agent_post_message('<task_id>', '<agent_id>', '<content>', '<idempotency_key>');
SELECT agent_post_message('<task_id>', '<agent_id>', 'NEEDS_INPUT_FOR_LEAD: missing=<fields>; attempted=<steps>; question=<exact_question>; unblock_condition=<needed_input>', '<idempotency_key>');
SELECT agent_log_action('<agent_id>', '<task_id>', '<action>', '<meta_json>', '<idempotency_key>');
SELECT agent_create_document('<task_id>', '<agent_id>', '<title>', '<content>');
SELECT agent_transition_task('<task_id>', 'in_progress', 'review', '<agent_id>', 'deliverable complete');
SELECT agent_transition_task('<task_id>', 'in_progress', 'blocked', '<agent_id>', '<reason>');
SELECT agent_update_status('<agent_id>', 'active');
```

Assignment wake payloads may arrive as legacy text (`Task <uuid> has been assigned to you`) or as a structured `TASK_ASSIGNMENT:` block.
Treat both as immediate pickup triggers and execute the same RPC-first sequence.

`agent_create_document` is strict 4-arg RPC only:
`SELECT agent_create_document('<task_id>', '<agent_id>', '<title>', '<content>');`
Never call 5-arg variants and never include MIME/type/path/URL arguments.
If you hit `function agent_create_document(... unknown, unknown, unknown, unknown, unknown) does not exist`,
retry once with the exact 4-arg call, then move task to `blocked` if it still fails.

Identity safety rules:
- Resolve your own `agent_id` at session start and cache it.
- Never hardcode UUIDs in write queries.
- Never reuse incoming `from_agent` as your own identity.
- Never pass placeholder strings like `'self'` to UUID RPC arguments; use a real UUID.

Forbidden schema guesses:
- `assigned_to`
- `assignee_id`
- `metadata`
- `messages` table

If missing task details prevent execution, request clarification through `agent_post_message` (this writes to `task_messages`) using the prefix `NEEDS_INPUT_FOR_LEAD:` and then move task to `blocked` with reason `needs input from lead`.

---

## Content Skills

Located in `/skills/`.

| Skill | Purpose |
|-------|---------|
| `copywriter` | UX/marketing copy — buttons, CTAs, emails, landing pages, error messages |
| `geo-optimizer` | Optimize content for AI citation (ChatGPT, Claude, Perplexity) |
| `content-gap-analysis` | Find competitor content gaps and opportunities |
| `seo-content-writer` | Write SEO-optimized blog posts and articles |
| `memory-setup` | Memory/recall system for agent continuity |

---

## Cloud Browser Tools

Use `cloud_browser_*` only when interactive/authenticated browsing is necessary.
For normal read-only research, prefer built-in fetch/search tools.

Available browser tools:
- `cloud_browser_list_profiles`
- `cloud_browser_create_profile`
- `cloud_browser_open`
- `cloud_browser_reset_profile`
- `cloud_browser_exec`
- `cloud_browser_request_takeover`
- `cloud_browser_resume`
- `cloud_browser_close`
