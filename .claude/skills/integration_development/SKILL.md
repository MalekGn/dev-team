---
name: integration_development
description: >-
  Backend-developer skill for integrating with third-party and external services.
  Use this whenever the server talks to something it doesn't control: external
  APIs, payment/email/storage providers, webhooks, or other internal services.
  Consult it before building ANY external integration so it's implemented per the
  architect's integration strategy and treats the dependency as unreliable —
  timeouts, retries, failure isolation, and secure credential handling — because
  an external service will fail, and it must not take your service down with it.
---

# Integration Development

Integrating with an external service means depending on something you don't
control — it will be slow, it will be down, it will change its behavior, all
without warning. The defining discipline is defensive: assume the dependency is
unreliable and make sure its failure degrades gracefully instead of cascading into
your service. This skill implements integrations per the architect's strategy, so
external faults stay contained.

## Follow the architect's integration strategy

The [[system_design]] integration strategy defines which external services are
used and how (sync vs. async, which boundaries). Implement that; don't add a new
external dependency on your own — introducing a vendor is an architecture decision.
If you need one that isn't in the design, raise it via [[communication]] to the
`software-architect`.

## Treat every external call as unreliable

Wrap external calls in the assumption that they can fail or hang:

```
- Timeouts        — every outbound call has one; never wait indefinitely
- Retries         — retry transient failures with backoff + jitter; cap attempts
- Idempotency     — ensure retries don't double-charge/double-send
- Circuit breaking — stop hammering a failing dependency; fail fast, recover later
- Fallback/degrade — define what happens when it's down (queue, default, clear error)
```

A missing timeout is the classic outage cause — one slow vendor exhausts your
connections and takes everything down ([[server_performance]]).

## Isolate the dependency behind an adapter

Wrap each external service in an adapter/client layer rather than scattering its
calls through your code. This gives you one place to handle auth, retries, error
mapping, and serialization — and it means the rest of your code depends on *your*
interface, not the vendor's, so swapping or mocking the vendor is localized.

## Handle credentials and data safely

- **Secrets outside code** — API keys/tokens from secure config, never committed
  ([[version_control]]); rotate-able.
- **Validate and map responses** — don't trust an external payload's shape;
  validate it and translate its errors into your contract's error envelope, never
  leaking vendor internals to your callers ([[auth_implementation]] for anything
  security-relevant).
- **Mind the data you send** — don't ship more user/PII data to a third party than
  the integration requires.

## Webhooks (inbound integrations)

If you receive callbacks: verify their authenticity (signatures), make handlers
idempotent (providers re-deliver), respond fast (offload work per
[[server_performance]]), and never trust the payload without validation.

## Verify

Test against the dependency's failure modes — timeout, error response, malformed
payload — not just its happy path, using mocks/stubs so tests don't hit the real
service. Failure handling is the whole point of an integration, so test it, per
[[backend_implementation]].
