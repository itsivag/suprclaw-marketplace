---
name: change-summary
description: Use when the user asks what changed, wants a changelog-style summary, repo/doc/thread delta, update digest, or before-and-after summary across available context.
metadata:
  version: 1.0.0
---

# Change Summary

Summarize what changed and why it matters.

## Sources

Use the provided context first. If connected tools are available and relevant, inspect docs, GitHub activity, emails, or research sources needed for the requested change window.

## Output Format

```markdown
# Change Summary

## Headline
- ...

## Changes
| Area | What changed | Source | Impact | Follow-up |
|---|---|---|---|---|

## Risks / Regressions To Watch
| Risk | Why | Owner | Suggested check |
|---|---|---|---|

## No Change / Unknown
| Area | Status | Note |
|---|---|---|

## Next Actions
1. ...
2. ...
3. ...
```

## Rules

- Do not infer changes without comparing sources or reading explicit updates.
- Keep facts and implications separate.
- If the source window is unclear, state the window used.
