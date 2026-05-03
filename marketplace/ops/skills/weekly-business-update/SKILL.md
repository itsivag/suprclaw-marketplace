---
name: weekly-business-update
description: Use when the user asks for a weekly business update, status report, weekly recap, investor-style update, team update, or summary of wins, changes, risks, priorities, and follow-ups.
metadata:
  version: 1.0.0
---

# Weekly Business Update

Turn the week's context into a structured business update that shows what changed, what matters, and what happens next.

## Output Format

```markdown
# Weekly Business Update - Week of YYYY-MM-DD

## Executive Summary
- ...

## Wins
| Win | Evidence | Impact |
|---|---|---|

## What Changed
| Area | Change | Source | Impact |
|---|---|---|---|

## Priorities For Next Week
| Priority | Owner | Due | Success criteria | Next action |
|---|---|---|---|---|

## Risks / Blockers
| Risk | Severity | Impact | Mitigation |
|---|---|---|---|

## Decisions Needed
| Decision | Context | Options | Recommended owner |
|---|---|---|---|

## Follow-Ups
| Follow-up | With | Why | Suggested timing |
|---|---|---|---|

## Metrics / Signals
| Signal | Current | Change | Note |
|---|---|---|---|

## Assumptions
- ...
```

## Rules

- Use a weekly window unless the user specifies a different period.
- Include only metrics or changes supported by provided context.
- Mark unknown metrics as `Not available`, not estimated.
- Keep recommendations actionable and tied to a next owner/action.
- Do not publish or send the update externally without explicit approval.
