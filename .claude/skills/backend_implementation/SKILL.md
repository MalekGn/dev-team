---
name: backend_implementation
description: >-
  Backend-developer skill for implementing server-side features — the general
  discipline of turning architect contracts and data models into working,
  maintainable server code. Use this whenever you build or modify server-side
  functionality: business logic, service structure, request handling, validation,
  and coordinating the sub-skills (endpoints, database, auth, performance,
  integrations). Consult it before writing ANY server code so implementation
  follows the architect's contracts and data model exactly rather than improvising
  either.
---

# Backend Implementation

The backend developer implements to two upstream artifacts — the architect's API
contracts and data model — and the core discipline is *fidelity to the contract*.
The frontend was built expecting exactly what the contract promises, so a server
that returns a different shape, or skips a defined error, breaks the client that
was built in parallel. This skill keeps server implementation faithful,
correct, and maintainable, and coordinates the specialized backend sub-skills.

## Build to the contract and the model

Before writing code, have both inputs:

- The [[api_contract_design]] contract — the exact request/response shapes and
  statuses your endpoints must honor.
- The [[data_modeling]] model — the entities, keys, and integrity rules your
  persistence must respect.

If either is missing or ambiguous, stop and raise a [[communication]]
`BLOCKED`/`QUESTION` — don't invent a contract or alter the schema on your own.
You implement to the architect's design; you don't define architecture.

## Correctness first: validate, handle errors, protect data

Server code is the enforcement boundary — the client's checks are only for UX, so
the server must not trust input:

- **Validate every input** at the boundary, per the contract's rules; reject
  invalid requests with the contract's error responses.
- **Handle failures explicitly** — return the defined error statuses; never leak
  stack traces or crash on a bad request.
- **Protect data integrity** — respect the model's constraints and use
  transactions where a unit of work must be all-or-nothing.

## Structure for maintainability

- **Separate concerns** — keep request handling ([[api_endpoint_development]]),
  business logic, and data access ([[database_access]]) in distinct layers so each
  is testable and changeable independently.
- **Keep logic idempotent and side-effect-aware** where the contract calls for it.
- **Match the codebase** — follow the established patterns, framework idioms, and
  the [[tech_stack_selection]] choices; read neighboring services first.

## Coordinate the sub-skills

Reach for the specialized skills explicitly:

- [[api_endpoint_development]] — implementing the endpoints themselves.
- [[database_access]] — persistence and queries.
- [[auth_implementation]] — authn/authz enforcement.
- [[server_performance]] — throughput, latency, caching.
- [[integration_development]] — third-party/service integrations.

## Verify and hand off

- Write unit/integration tests for your own services (the `qa-engineer` owns
  overall strategy, not your service tests).
- Verify responses match the contract — success *and* error paths — before PR.
- Commit and PR per [[version_control]] and [[documentation]], referencing the
  contract and model you implemented. Stay in scope: no UI, no client code, no
  architecture decisions — route those via [[communication]].
