# TOOLS.md - Growth Worker Typed Supabase Contract

SPECIALIST_PROFILE:growth
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

## Growth Execution Defaults

If the brief is incomplete, make explicit assumptions and continue.
Recommended defaults for the first execution cycle:

- `target_audience`: founders, operators, or the audience stated in the task
- `objective`: attention and qualified demand
- `channels`: LinkedIn, X, Facebook, TikTok, Reels
- `formats`: short-form video script, social post, hook set, content calendar, competitor pattern brief
- `tone`: direct, useful, specific, non-hype
- `measurement`: views, saves, replies, clicks, conversions, or qualified conversations

Post assumptions with `mcp_supabase_post_message(caller_id=<supabase_uuid>, ...)` before continuing.

---

## Growth Skills

Use local `/skills/*` for specialist growth work. Pick the narrowest relevant skill before producing output:

- trend and channel work: `social-content`, `content-strategy`, `marketing-ideas`, `community-marketing`
- competitor work: `competitor-profiling`, `competitor-alternatives`, `customer-research`
- conversion and copy: `copywriting`, `landing-page-copywriting` if present, `page-cro`, `form-cro`, `signup-flow-cro`, `onboarding-cro`
- campaigns and distribution: `launch-strategy`, `directory-submissions`, `referral-program`, `email-sequence`, `cold-email`, `paid-ads`
- SEO and AI discovery: `seo-audit`, `ai-seo`, `programmatic-seo`, `schema-markup`
- lifecycle and monetization: `churn-prevention`, `pricing-strategy`, `paywall-upgrade-cro`, `revops`, `sales-enablement`

Keep Mission Control coordination in the typed Supabase tools listed above.
