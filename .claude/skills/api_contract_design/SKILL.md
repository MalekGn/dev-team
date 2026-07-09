---
name: api_contract_design
description: >-
  Software-architect skill for designing API contracts — the precise interfaces
  between client and server and between services. Use this whenever you define or
  revise an endpoint/operation: its request and response schemas, status codes,
  error formats, auth, versioning, and pagination. Consult it before developers
  build against an interface so the contract is complete and unambiguous — the
  frontend and backend implement to it independently, and QA validates against
  it, so gaps here become bugs everywhere.
---

# API Contract Design

The contract is the seam that lets frontend and backend developers work in
parallel without talking constantly — both build to the same agreed interface,
and QA validates against it. That only works if the contract is complete: every
field, every status, every error. An underspecified contract ("returns the
user") sends two developers off with different mental models and guarantees an
integration bug. This skill makes the interface exact before anyone builds it.

## Design the contract before the implementation

The contract comes from [[system_design]] boundaries and
[[requirement_analysis]] requirements, and it precedes implementation. You define
the interface; the `backend-developer` implements the server side and the
`frontend-developer` the client side — neither invents the shape. Keep it about
*what crosses the boundary*, not how the server fulfills it.

## Specify every operation completely

For each endpoint/operation, pin down all of it:

```
OPERATION: <name / METHOD path>
purpose: <what it does, one line>
request:
  - path/query params  (name, type, required?, constraints)
  - body schema        (fields, types, required?, validation rules)
request auth: <who may call it; scopes/roles>
responses:
  - success: status + body schema
  - errors:  status per case + error body shape + when it occurs
idempotency: <safe to retry? idempotency key?>
pagination/filtering: <if a collection — how>
```

The error cases are not optional — most integration pain lives in unspecified
failure responses.

## Consistency across the surface

An API is learned as a whole, so make it predictable:

- **Uniform error shape** — one error envelope everywhere (code, message,
  details), not a different shape per endpoint.
- **Consistent conventions** — naming, casing, date/time format, IDs, and
  pagination style are the same across all operations.
- **Standard status codes** used correctly (200/201/204, 400/401/403/404/409,
  5xx) so clients handle them generically.

## Contracts are stable promises

- **Version deliberately.** Once developers build to a contract, changing it
  breaks them — additive changes are safe; breaking changes need a new version.
- **Validate at the boundary.** Specify what the server must reject and how;
  server-side validation is the backend developer's to implement, per this spec.
- **Record consequential API decisions** in an [[adr_writing]] ADR.

## Handing off

Publish contracts per the [[documentation]] API-contract structure with concrete
request/response examples, at a predictable path. They drive
[[data_modeling]], the developers' implementation, and QA's validation — a change
to a contract is announced via [[communication]] so both sides re-sync.
