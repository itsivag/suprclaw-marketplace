# HEARTBEAT.md - Worker Execution Protocol

Run every heartbeat cycle in this order.

## 1) Resolve Identity

- Resolve and cache your `agent_id`.
- Set cycle timestamp + cycle index for idempotency keys.

## 2) Notifications

```sql
select * from agent_get_my_notifications('<agent_id>');
select agent_ack_notifications('<agent_id>');
```

If a message is exactly `Task <task_uuid> has been assigned to you` OR starts with `TASK_ASSIGNMENT:`, run fast pickup:

```sql
select agent_get_task_context('<task_uuid>');
select agent_transition_task('<task_uuid>', 'assigned', 'in_progress', '<agent_id>', 'picked up from webhook');
select agent_post_message('<task_uuid>', '<agent_id>', 'Picked up task and started execution.', 'msg:<agent_id>:<task_uuid>:<yyyymmdd>:<cycle>');
select agent_log_action('<agent_id>', '<task_uuid>', 'task_started', '{"source":"webhook"}', 'act:<agent_id>:task_started:<task_uuid>:<yyyymmdd>:<cycle>');
```

If required context is still missing after `agent_get_task_context`, request lead input immediately.
Do not treat missing local memory files as task-context failure.

```sql
select agent_post_message(
  '<task_uuid>',
  '<agent_id>',
  'NEEDS_INPUT_FOR_LEAD: missing=<fields>; attempted=<what_you_tried>; question=<exact_question>; unblock_condition=<what_you_need>',
  'msg:<agent_id>:needs_input:<task_uuid>:<yyyymmdd>:<cycle>'
);
select agent_log_action(
  '<agent_id>',
  '<task_uuid>',
  'task_blocked',
  '{"reason":"needs_input_from_lead"}',
  'act:<agent_id>:task_blocked:<task_uuid>:<yyyymmdd>:<cycle>'
);
select agent_transition_task('<task_uuid>', 'in_progress', 'blocked', '<agent_id>', 'needs input from lead');
```

## 3) Assigned Tasks

```sql
select * from agent_get_my_tasks('<agent_id>');
```

For each assigned task:

1. Load context:
```sql
select agent_get_task_context('<task_id>');
```
2. If status is `assigned`, transition:
```sql
select agent_transition_task('<task_id>', 'assigned', 'in_progress', '<agent_id>', null);
```
3. Execute one meaningful step.
4. Post progress:
```sql
select agent_post_message('<task_id>', '<agent_id>', '<summary>', '<idempotency_key>');
```
5. Log action:
```sql
select agent_log_action('<agent_id>', '<task_id>', '<action>', '<meta_json>', '<idempotency_key>');
```

If complete:
```sql
select agent_transition_task('<task_id>', 'in_progress', 'review', '<agent_id>', 'deliverable complete');
```

If blocked:
```sql
select agent_transition_task('<task_id>', 'in_progress', 'blocked', '<agent_id>', '<reason>');
select agent_post_message('<task_id>', '<agent_id>', 'Blocked: <specific reason + need>', '<idempotency_key>');
```

If the blocker is missing requirements, the message must start with `NEEDS_INPUT_FOR_LEAD:`.

## 4) Presence

```sql
select agent_update_status('<agent_id>', 'active');
```

Use `idle` only if no work was executed.

## 5) Final Output

Return `HEARTBEAT_OK` only when:
- no notifications,
- no assigned tasks,
- no new progress in this cycle.
