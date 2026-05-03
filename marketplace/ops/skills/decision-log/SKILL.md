---
name: decision-log
description: Use when the user wants to organize decisions, capture what was decided, track rationale, create a decision log, or separate decisions from notes and action items.
metadata:
  version: 1.0.0
---

# Decision Log

Create or update a structured record of decisions and their operational consequences.

## Output Format

```markdown
# Decision Log

| Date | Decision | Context | Rationale | Owner | Impact | Follow-up / Review |
|---|---|---|---|---|---|---|

## Open Decisions
| Decision needed | Options | Owner | Needed by | Blocking |
|---|---|---|---|---|

## Revisit Later
| Decision | Revisit trigger | Notes |
|---|---|---|
```

## Rules

- Include only decisions actually made or explicitly needed.
- Do not convert opinions into decisions unless the source makes commitment clear.
- If rationale is missing, mark `Rationale not captured`.
- Include operational impact and follow-up when available.
