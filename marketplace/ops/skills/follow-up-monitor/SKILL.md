---
name: follow-up-monitor
description: Use when the user asks what they have not followed up on, who needs a response, stale threads, pending replies, waiting items, or open loops across notes, email, GitHub, tasks, and docs.
metadata:
  version: 1.0.0
---

# Follow-Up Monitor

Identify open loops and recommend follow-up actions.

## Signals

Look for:

- Explicit promises: "I'll", "we should", "follow up", "circle back", "send", "check"
- Questions waiting for an answer
- Blocked tasks waiting on someone
- Emails/messages that appear to require reply
- PRs/issues waiting on review or action
- Deadlines mentioned without completion evidence
- Decisions with no owner or next step

## Output Format

```markdown
# Follow-Up Review

## Highest Priority Follow-Ups
| Priority | Follow-up | With | Source | Since | Why it matters | Suggested next step |
|---|---|---|---|---|---|---|

## Waiting On Others
| Person/team | Waiting on | Since | Risk | Recommended timing |
|---|---|---|---|---|

## You May Owe
| Recipient | Owed item | Source | Draft follow-up |
|---|---|---|---|

## Low Confidence / Needs Confirmation
| Item | Why uncertain | Clarifying question |
|---|---|---|
```

## Rules

- Do not claim a follow-up is overdue without a date or clear staleness signal.
- Do not send follow-ups automatically.
- Draft follow-up language only when useful.
- Separate high-confidence follow-ups from low-confidence possible loops.
