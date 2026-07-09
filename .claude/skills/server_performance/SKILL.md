---
name: server_performance
description: >-
  Backend-developer skill for keeping the server fast, efficient, and resilient
  under load. Use this whenever server-side performance or robustness matters:
  latency and throughput, caching, connection/resource pooling, async/background
  work, and graceful error handling under load. Consult it before shipping ANY
  performance-sensitive server work so it's engineered against the architect's NFR
  targets and measured — optimizing real, profiled bottlenecks rather than guessed
  ones, without sacrificing correctness.
---

# Server Performance

Server performance multiplies: one slow endpoint slows every user who hits it, and
a resource leak that's invisible in dev takes the service down under real load. As
on the client, intuition about where the time goes is usually wrong — so this
skill engineers server speed against the architect's targets and *measures*,
optimizing profiled bottlenecks rather than imagined ones, and never trading away
correctness for speed.

## Optimize against targets, and measure

The [[nfr_definition]] NFRs set the bar — latency percentiles, throughput at a
given load. Treat those as the goal, profile to find the actual bottleneck, change
it, and confirm the number moved. A "faster" change with no measurement is a
guess, and often a wrong one.

## The database is usually first

Most backend latency is data access, so look there before micro-optimizing code:

- **Fix N+1 and unindexed queries** ([[database_access]]) — the single most common
  server bottleneck.
- **Fetch only what's needed** and paginate large results.
- **Pool connections** — don't open/close per request.

## Cache deliberately

Caching is powerful and dangerous — stale or wrongly-scoped caches serve wrong
data. When you cache:

- Cache what's read-often and changes-rarely; skip it for volatile or
  user-specific-sensitive data unless scoped correctly.
- Define **invalidation** up front — when does the cached value become wrong, and
  how is it refreshed? A cache without an invalidation story is a bug factory.
- Respect the [[api_contract_design]] semantics (don't cache past what the
  contract allows).

## Do slow work off the request path

If work is slow but the caller doesn't need its result synchronously, move it to
a background job/queue and return promptly — per the [[system_design]] async
strategy. Keep the request path doing only what the response actually requires.

## Resilient under load

Performance includes not falling over:

- **Bound resources** — connection/thread pools, timeouts on every outbound call
  so one slow dependency doesn't exhaust the server.
- **Fail gracefully** — apply timeouts, retries with backoff, and circuit
  breaking for [[integration_development]] dependencies; degrade rather than
  cascade.
- **Guard against overload** — rate limiting/backpressure where the NFRs require.

## Don't over-optimize, and stay in scope

Optimize what the profile and targets say matters; leave the rest simple, since
complexity has its own maintenance cost. If meeting a target needs an
architectural change (scaling approach, new caching tier), that's the architect's
call — raise it via [[communication]] rather than contorting the service. Verify
correctness is intact ([[backend_implementation]]) and note before/after
measurements in the [[version_control]] PR.
