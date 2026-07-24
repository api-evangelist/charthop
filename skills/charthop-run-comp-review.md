---
name: Run a ChartHop compensation review
description: Create and manage a compensation review cycle, including comp bands and approvals.
api: openapi/charthop-openapi-original.json
operations: [findCompReviews, createCompReview, getCompReviewById, updateCompReview, findCompBands, getApprovalRequestsForCompReview]
---

# Run a ChartHop compensation review

Drive a comp-review cycle through the ChartHop API.

## Auth
`Authorization: Bearer <app authorization token>`; all operations are org-scoped by
`{orgId}`. Base URL: `https://api.charthop.com`.

## Steps
1. **List existing cycles** — `findCompReviews` (`GET`) to see current/past reviews.
2. **Create a cycle** — `createCompReview` (`POST`) with the review definition.
3. **Read a cycle** — `getCompReviewById` (`GET .../{compReviewId}`).
4. **Update a cycle** — `updateCompReview` (`PATCH .../{compReviewId}`).
5. **Reference comp bands** — `findCompBands` (`GET`) to anchor recommendations to salary
   bands; `getCompBandSchema` / `getCompBandById` for detail.
6. **Track approvals** — `getApprovalRequestsForCompReview` to follow the approval chain.

## Conventions
- Offset/limit pagination (`from`, `limit`); sparse fields via `fields`; CQL `filter`.
- No idempotency key — dedupe cycle creation client-side.
- Errors are `{"code","message"}`; expect 403 for insufficient comp permissions.
