---
name: api_endpoint_development
description: >-
  Backend-developer skill for implementing API endpoints to the architect's
  contracts. Use this whenever you build or modify a server endpoint: routing,
  parsing and validating requests, invoking business logic, and returning the
  exact responses and status codes the contract defines. Consult it before
  implementing ANY endpoint so it honors the contract precisely — request shape,
  every response status, error format, and auth — because the client was built
  against that same contract.
---

# API Endpoint Development

An endpoint is the concrete realization of a [[api_contract_design]] contract, and
the client was built against that contract's exact promises. So endpoint work is
conformance work: return precisely the shapes, statuses, and errors the contract
defines. An endpoint that "mostly" matches — a renamed field, an unhandled 409 —
is an integration bug waiting for the client. This skill implements endpoints that
honor the contract exactly.

## Implement the contract precisely

For each endpoint, match the contract point for point:

```
- route/method       — exactly as specified
- request parsing    — path/query/body per the contract's schema
- validation         — enforce every documented rule; reject with the defined error
- auth               — enforce who may call it ([[auth_implementation]])
- success response   — the exact body + status (200/201/204…)
- error responses    — every documented case, with the standard error envelope
```

If reality demands something the contract doesn't cover, that's a contract change
— raise it via [[communication]] to the `software-architect`; don't quietly
diverge.

## The endpoint is a thin boundary

Keep the endpoint layer thin: parse, validate, authorize, delegate to business
logic, and shape the response. Business rules and persistence live behind it (in
services and [[database_access]]), so the same logic is reusable and testable
without going through HTTP. A fat endpoint with logic inline is hard to test and
duplicates itself across routes.

## Validate and fail correctly

- **Never trust the request.** Validate at the boundary regardless of what the
  client claims to have checked — the server is the real enforcement point.
- **Use the right status codes** — 400 for bad input, 401/403 for auth, 404 for
  missing, 409 for conflict, 422 for semantic validation, 5xx for server faults —
  as the contract specifies, so clients handle them generically.
- **Return the standard error envelope** the contract defines; don't invent a
  per-endpoint error shape or leak internals/stack traces.

## Idempotency, concurrency, and safety

Honor the contract's idempotency guarantees (safe retries for the same request),
and guard against concurrent-request races on shared data with transactions or
appropriate locking (coordinate with [[data_modeling]] integrity rules). Costly or
destructive operations get extra care — confirmations, soft-deletes where the
model calls for it.

## Verify and hand off

Test each endpoint against the contract's success *and* error cases (integration
tests hitting the route), per [[backend_implementation]]. Commit/PR referencing the
contract per [[version_control]] and [[documentation]]; the `qa-engineer`
validates the endpoint against the same contract.
