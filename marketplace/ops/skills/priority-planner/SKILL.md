---
name: priority-planner
description: Use when the user asks what to prioritize, how to order tasks, what to do first, how to plan the day/week, or how to rank competing work by urgency, importance, dependencies, and business impact.
metadata:
  version: 1.0.0
---

# Priority Planner

Rank work and produce a clear execution order.

## Priority Model

Score each item using:

- Urgency: time sensitivity or deadline pressure
- Importance: business/user impact
- Dependency: whether other work is blocked by it
- Risk: cost of delay or failure
- Effort: rough effort when known
- Confidence: how complete the available context is

## Output Format

```markdown
# Priority Plan

## Recommended Order
1. **[Task]** - rationale and next action
2. **[Task]** - rationale and next action
3. **[Task]** - rationale and next action

## Priority Table
| Rank | Task | Urgency | Impact | Dependency | Risk | Effort | Owner | Due | Next action |
|---|---|---|---|---|---|---|---|---|---|

## Defer / Later
| Task | Why deferred | Revisit trigger |
|---|---|---|

## Blocked
| Task | Blocker | Needed to unblock |
|---|---|---|

## Assumptions
- ...
```

## Rules

- Explain why the top three are top three.
- Do not over-optimize vague items; turn them into concrete next actions.
- If everything appears urgent, identify the constraint or dependency that matters most.
