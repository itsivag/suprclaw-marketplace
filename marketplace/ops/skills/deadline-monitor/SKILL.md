---
name: deadline-monitor
description: Use when the user asks about deadlines, overdue work, upcoming commitments, what is due this week, what is at risk, or time-sensitive business items.
metadata:
  version: 1.0.0
---

# Deadline Monitor

Review deadlines and time-sensitive commitments, then surface what needs action.

## Process

1. Extract all dates, relative timing, deadlines, and milestones from available context.
2. Normalize dates when possible using the current date and timezone from user context.
3. Group items into overdue, due today, due this week, upcoming, and unscheduled.
4. Identify blockers and owner gaps.
5. Recommend next actions.

## Output Format

```markdown
# Deadline Review

## Overdue
| Item | Due | Owner | Status | Risk | Next action |
|---|---|---|---|---|---|

## Due Today
| Item | Owner | Status | Next action |
|---|---|---|---|

## Due This Week
| Item | Due | Owner | Risk | Next action |
|---|---|---|---|---|

## Upcoming
| Item | Due | Prep needed |
|---|---|---|

## Needs Scheduling
| Item | Why it needs a date | Suggested owner |
|---|---|---|
```

## Rules

- Use exact dates when the source provides them.
- If relative dates are ambiguous, state the assumption.
- Do not reschedule, create reminders, or update external systems without approval.
