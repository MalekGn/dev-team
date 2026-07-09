---
name: state_management
description: >-
  Frontend-developer skill for managing client-side state and data flow. Use this
  whenever you decide where state lives and how it updates: local vs. shared vs.
  server-cache state, data flow between components, derived state, and keeping UI
  in sync with the backend. Consult it before wiring ANY non-trivial stateful
  behavior so state is scoped at the right level, has a single source of truth,
  and stays predictable rather than sprawling into tangled, hard-to-debug updates.
---

# State Management

State is where frontend complexity concentrates — most confusing UI bugs are
really state bugs: two copies of the same fact disagreeing, an update that races,
a stale cache. The discipline is to keep each piece of state at the right scope
with a single source of truth, so behavior stays predictable. This skill decides
where state lives and how it flows before the tangle forms.

## Scope state as narrowly as it can live

State pushed higher than it needs to be couples unrelated components and causes
needless re-renders; state kept too low forces awkward lifting later. Default to
the narrowest scope that works:

```
- Local (component)     — UI-only concerns: open/closed, input focus, hover
- Shared (feature)      — state several components in a feature need
- Global (app)          — genuinely app-wide: session, theme, current user
- Server-cache          — data owned by the backend, cached client-side
```

Don't reach for global state by reflex — most state is local.

## One source of truth per fact

Every piece of state has exactly one owner; everything else derives or reads from
it. Two components each holding their own copy of "the current project" will drift
out of sync — the classic state bug. Derive computed values from the source
instead of storing them separately.

## Server data is a cache, not local state

Data from the backend (via [[api_integration_client]]) is a *cache* of a remote
source of truth, and treating it as plain local state is a recipe for staleness.
Handle it as cache: track loading/error/success, decide when to refetch or
invalidate, and reconcile after mutations. Coordinate the optimistic-vs-confirmed
update behavior with the [[interaction_design]] spec.

## Keep updates predictable

- **Unidirectional flow** — data flows down, events flow up; avoid two-way tangles
  that make cause and effect hard to trace.
- **Immutable updates** — produce new state rather than mutating in place, so
  changes are traceable and rendering is reliable.
- **Isolate side effects** — keep effects (fetches, subscriptions) out of pure
  render/derive logic.

## Match the project's approach

Use whatever state solution the [[tech_stack_selection]] and existing codebase
already establish — don't introduce a new state library on your own; that's an
architecture-level choice. Raise it via [[communication]] if the current approach
genuinely doesn't fit.

## Verify

Cover reducers/derivations and update logic with unit tests, per
[[frontend_implementation]]. State transitions are highly testable and a common
defect source — test them.
