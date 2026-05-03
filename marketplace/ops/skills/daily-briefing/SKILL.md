---
name: daily-briefing
description: Use when the user asks for today's priorities, a morning briefing, daily command center, what needs attention, inbox/calendar/task recap, or a concise operating plan for the day.
metadata:
  version: 1.0.0
---

# Daily Briefing

Create a concise command-center briefing that helps the user decide what to do next today.

## Inputs To Use

Use only available context: user notes, chat history, memory files, task context, documents, and connected-tool summaries when available. Do not invent calendar events, emails, deadlines, or task statuses.

If connected tools are available and relevant, read before summarizing:

- Gmail for emails that need reply or review
- GitHub for issues, PRs, reviews, failing checks, or repo activity
- memory files for prior priorities and open loops
- web/research only when the briefing needs external current information

## Output Format

```markdown
# Daily Briefing - YYYY-MM-DD

## Top Priorities
| Priority | Item | Why it matters | Owner | Due | Next action |
|---|---|---|---|---|---|

## Needs Attention
| Item | Signal | Risk | Recommended action |
|---|---|---|---|

## Waiting / Follow-Ups
| Person or area | Waiting on | Since | Follow-up draft or next step |
|---|---|---|---|

## Blockers
| Blocker | Impact | Needed to unblock |
|---|---|---|

## Time-Sensitive Items
| Deadline | Item | Status | Action |
|---|---|---|---|

## Suggested Order
1. ...
2. ...
3. ...

## Assumptions
- ...
```

## Rules

- Rank priorities by urgency, importance, risk, and dependency impact.
- Mark missing owner or date as `TBC`.
- Separate facts from recommendations.
- Keep the briefing short enough to scan in under two minutes unless the user asks for detail.
- Do not send messages, change task status, archive email, or mutate external systems without explicit approval.
