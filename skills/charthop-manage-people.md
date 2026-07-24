---
name: Manage the ChartHop people roster
description: Read, create, and update people (employees) in a ChartHop org via the REST API.
api: openapi/charthop-openapi-original.json
operations: [findPersons, getPerson, createPerson, updatePerson, getOrgUsersAndPeople]
---

# Manage the ChartHop people roster

Programmatically keep an org's roster in sync with ChartHop.

## Auth
Send `Authorization: Bearer <app authorization token>` on every request (see
`authentication/charthop-authentication.yml`). All operations are org-scoped by `{orgId}`.
Base URL: `https://api.charthop.com`.

## Steps
1. **List people** — `findPersons` (`GET /v2/org/{orgId}/person`). Narrow results with
   the `q` search param, a CQL `filter`, `sort`, and select columns with `fields`. Page
   with `from` (offset) + `limit`.
2. **Read one person** — `getPerson` (`GET /v2/org/{orgId}/person/{personId}`).
3. **Create a person** — `createPerson` (`POST /v2/org/{orgId}/person`) with the person
   body (name, work email, job, department, start date).
4. **Update a person** — `updatePerson` (`PATCH /v2/org/{orgId}/person/{personId}`) with
   only the changed fields.
5. **Reconcile users + people** — `getOrgUsersAndPeople`
   (`GET /v1/org/{orgId}/data-users-persons`) to map platform users to person records.

## Conventions
- Pagination is offset/limit (`from`, `limit`) — no cursors.
- There is **no idempotency key**; guard create/update retries on the client side.
- Errors return `{"code": <int>, "message": <string>}` — see
  `errors/charthop-problem-types.yml`. Handle 401/403 (permissions), 404, 409 (conflict).
