---
name: api_integration_client
description: >-
  Frontend-developer skill for integrating the client with backend APIs per the
  architect's contracts. Use this whenever you call an API from the client: making
  requests to the defined endpoints, handling responses and every error status,
  managing auth tokens, and mapping API data to the UI. Consult it before wiring
  ANY client-server call so the integration matches the contract exactly, handles
  failures gracefully, and never assumes a shape the contract doesn't define.
---

# API Integration Client

The API contract is the agreement that lets the frontend and backend be built in
parallel — so on the client side, integration means implementing *exactly* to
that contract. The failure mode is assuming a shape the contract doesn't
guarantee (a field that's sometimes null, an error status never handled), which
works in the demo and breaks in production. This skill keeps the client's use of
the API faithful and failure-tolerant.

## Implement to the contract, exactly

Call endpoints as the [[api_contract_design]] contract defines them — methods,
paths, params, request bodies, and the response shapes per status code. Don't
depend on undocumented behavior; if you need something the contract doesn't
provide, that's a contract change — raise it via [[communication]] to the
`software-architect`, don't work around it with a fragile assumption.

## Handle every response, not just 200

The contract lists the error statuses for a reason — each needs client behavior:

```
- success (2xx)      — map to state per [[state_management]]
- validation (400)   — surface field errors to the user
- auth (401/403)     — trigger re-auth or an access message
- not found (404)    — the appropriate empty/error UI
- conflict (409)     — reconcile per the interaction spec
- server (5xx)       — user-facing error + retry affordance
- network failure    — offline/timeout handling, not an unhandled throw
```

Every branch maps to a state the [[interaction_design]] and [[wireframing]] specs
already define — wire them, don't invent new ones.

## Centralize the API layer

Keep API access behind a single client layer rather than scattering fetch calls
through components. One place to handle base URL, headers, auth, serialization,
and error normalization means consistent behavior and one place to change when the
contract versions. Components consume typed results, not raw responses.

## Auth and security on the client

- Attach credentials/tokens per the contract's auth scheme; handle token refresh
  and expiry centrally.
- Store tokens per the security approach the architect defined — don't invent
  your own storage scheme.
- Never trust the client as the security boundary: client validation is for UX;
  the real enforcement is the backend's ([[auth_implementation]]). Mirror the
  contract's validation rules for fast feedback, but assume the server re-checks.

## Verify

Test the integration against the contract's success and error responses (mock the
API), per [[frontend_implementation]]. Handle loading/latency via
[[state_management]], and commit/PR referencing the contract per
[[version_control]] and [[documentation]].
