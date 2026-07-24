---
name: Track goals and progress in ChartHop
description: Create goals, record progress, and manage goal types via the ChartHop API.
api: openapi/charthop-openapi-original.json
operations: [findGoals, createGoal, findGoalProgress, createGoalProgress, updateGoalProgress, findGoalTypes]
---

# Track goals and progress in ChartHop

Manage OKR/goal data programmatically.

## Auth
`Authorization: Bearer <app authorization token>`; org-scoped by `{orgId}`. Base URL:
`https://api.charthop.com`.

## Steps
1. **List goals** — `findGoals` (`GET`) filtered by owner/person, group, or CQL `filter`.
2. **Create a goal** — `createGoal` (`POST`) with title, owner, target, and goal type
   (see `findGoalTypes`).
3. **List progress** — `findGoalProgress` (`GET`) for a goal's progress records.
4. **Record progress** — `createGoalProgress` (`POST`) to append a progress update.
5. **Update progress** — `updateGoalProgress` (`PATCH .../{...}`) to correct an entry.

## Conventions
- Offset/limit pagination (`from`, `limit`); `fields` for sparse responses.
- No idempotency key — avoid duplicate progress posts on retry.
- Errors are `{"code","message"}` — see `errors/charthop-problem-types.yml`.
