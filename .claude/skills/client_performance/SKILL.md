---
name: client_performance
description: >-
  Frontend-developer skill for keeping the client fast and responsive. Use this
  whenever performance matters on the client: load time and bundle size, render
  performance and avoiding unnecessary re-renders, lazy-loading, asset
  optimization, and perceived performance. Consult it before shipping ANY
  performance-sensitive client work so speed is engineered against the architect's
  NFR targets and measured, not guessed at — and so optimization targets real
  bottlenecks instead of imagined ones.
---

# Client Performance

Client performance is what the user actually feels — a correct app that's slow
feels broken. But performance work is uniquely prone to wasted effort:
optimizing the wrong thing is common because intuition about bottlenecks is
usually wrong. This skill engineers client speed against the architect's targets
and *measures* before and after, so effort goes where it moves the number.

## Optimize against targets, and measure

The [[nfr_definition]] NFRs set the client performance bar (load time, interaction
latency). Treat those as the goal, and measure against them — profile to find the
real bottleneck before changing code, and confirm the change actually helped.
"Faster-feeling" without a measurement is how effort gets spent on non-problems.

## The usual bottlenecks, in order

Most client slowness comes from a short list — check these first:

```
- Bundle size        — too much JS shipped/parsed up front
- Unnecessary work   — re-renders, recomputation, work in loops/effects
- Network            — too many/too large requests, no caching, waterfalls
- Assets             — unoptimized images/fonts, no lazy-loading
- Blocking main thread — heavy synchronous work janking the UI
```

## Load less, later

- **Split and lazy-load** — ship what the first view needs; defer the rest
  (route/component-level code splitting).
- **Optimize assets** — right-sized, modern-format, lazy-loaded images; subset
  fonts. Especially important for the mobile targets ([[responsive_implementation]]
  — don't send desktop-weight assets to phones).
- **Cache** — leverage the [[api_integration_client]] cache and HTTP caching;
  avoid refetching unchanged data.

## Render efficiently

- Avoid needless re-renders — stable references, memoization *where profiling
  shows it helps* (not sprinkled everywhere, which adds its own cost).
- Keep [[state_management]] updates narrow so a change re-renders only what
  depends on it.
- Virtualize large lists; keep expensive work off the main thread.

## Don't over-optimize

Premature optimization adds complexity that makes code harder to maintain for
speed nobody notices. Optimize what the measurement and the NFR targets say
matters; leave the rest simple. If hitting a target requires an architectural
change (not just client tuning), raise it via [[communication]] to the
`software-architect` rather than contorting the client.

## Verify and hand off

Confirm the change against the target with a real measurement, note the
before/after in the [[version_control]] PR, and keep [[frontend_implementation]]
correctness intact — a fast screen that drops a state is still broken.
