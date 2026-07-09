---
name: auth_implementation
description: >-
  Backend-developer skill for implementing authentication and authorization on
  the server. Use this whenever you handle identity or access control: verifying
  who a caller is (authn), enforcing what they may do (authz), managing sessions
  or tokens, protecting credentials, and applying the security model to endpoints.
  Consult it before implementing ANY auth-related server code so it enforces the
  architect's security model correctly — the server is the real security
  boundary, and auth bugs are among the most damaging defects possible.
---

# Auth Implementation

Auth is the highest-stakes code the backend developer writes: a mistake doesn't
degrade the product, it exposes user data or lets the wrong person act. And it
must live on the server, because the client can be bypassed entirely — client
checks are UX, server checks are security. This skill implements authn and authz
to the architect's security model, on the assumption that everything reaching the
server is potentially hostile.

## Enforce the architect's security model

The [[nfr_definition]] and [[api_contract_design]] define the security scheme —
auth method, who may call each endpoint, what scopes/roles exist. Implement that
model; don't invent your own scheme. If it's unspecified for something you're
building, stop and get it from the `software-architect` via [[communication]] —
guessing at auth is how holes are created.

## Authentication: prove who the caller is

- **Verify identity on every protected request** — validate the token/session
  server-side (signature, expiry, issuer); never trust a client-supplied identity
  claim at face value.
- **Manage tokens/sessions correctly** — sensible expiry, refresh, and
  revocation; invalidate on logout and on credential change.
- **Protect credentials** — hash passwords with a strong adaptive algorithm
  (never plaintext or fast hashes); store secrets/keys outside code and config in
  the clear.

## Authorization: enforce what they may do

Authentication is not authorization — knowing *who* someone is doesn't mean they
may do *this*:

- **Check permission on every action**, at the server, against the resource being
  acted on — not just "is logged in."
- **Prevent object-level bypass (IDOR)** — verify the caller actually owns/may
  access the specific record, not just that the endpoint is protected. This is one
  of the most common and damaging real-world flaws.
- **Deny by default** — no matching grant means refused; return the contract's
  401 (unauthenticated) vs. 403 (forbidden) correctly, without leaking whether a
  resource exists when that itself is sensitive.

## Guard against the common attacks

```
- Injection        — parameterize all queries ([[database_access]])
- Broken access     — enforce authz per-object, server-side, every time
- Sensitive exposure — encrypt in transit; don't log tokens/passwords/PII
- Brute force        — rate-limit and lock out repeated auth failures
- CSRF/session       — apply the protections the security model specifies
```

## Verify carefully

Auth deserves more test rigor than typical code: test the *negative* paths
explicitly — expired/tampered tokens, missing permission, accessing another
user's resource, and privilege boundaries — per [[backend_implementation]]. A
passing happy-path auth test proves almost nothing; the denials are the point.
Commit/PR per [[version_control]], and flag any security concern to the architect
and `qa-engineer` via [[communication]].
