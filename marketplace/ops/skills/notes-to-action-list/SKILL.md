---
name: notes-to-action-list
description: Use when the user gives messy notes, brainstorms, chat fragments, docs, or rough ideas and wants them converted into tasks, priorities, next steps, or an action plan.
metadata:
  version: 1.0.0
---

# Notes To Action List

Convert unstructured notes into a clear execution list.

## Process

1. Extract concrete tasks, decisions, blockers, questions, deadlines, and owners.
2. Deduplicate repeated items.
3. Group related tasks by workstream.
4. Rank by urgency, dependency, and business impact.
5. Mark missing owner/date/status as `TBC`.
6. Preserve source wording when ambiguity matters.

## Output Format

```markdown
# Action List

## Summary
- ...

## Tasks
| Priority | Task | Owner | Due | Status | Blocker | Next action |
|---|---|---|---|---|---|---|

## Decisions
| Decision needed | Context | Owner | Due |
|---|---|---|---|

## Open Questions
| Question | Why it matters | Who can answer |
|---|---|---|

## Follow-Ups
| Follow-up | With | Suggested timing | Draft note |
|---|---|---|---|

## Assumptions
- ...
```

## Rules

- Do not create fake tasks from vague sentiment; label vague items as questions or notes.
- If a note implies an action but lacks details, create the smallest safe next action.
- Do not mark any task complete unless the source explicitly says it is complete.
