---
name: backlog_management
description: >-
  Product-manager skill for building and grooming a prioritized product backlog.
  Use this whenever you create, order, refine, or triage backlog items — writing
  well-formed stories, applying a prioritization framework (RICE, MoSCoW,
  value-vs-effort), keeping items ready for the next stage, and pruning stale
  work. Consult it before ANY prioritization or grooming decision so the backlog
  stays ordered by explicit criteria, items are "ready" before they're pulled in,
  and priority calls are transparent and defensible.
---

# Backlog Management

The backlog is the single ordered queue of what to build next. Its value is that
the top is always the most important, well-understood, ready-to-start work — so
design, architecture, and the developers can pull from the top with confidence.
A backlog ordered by gut feel, full of vague items, forces everyone downstream to
re-litigate priority. This skill keeps the queue ordered by explicit criteria and
every item ready before it's pulled.

## Prioritize with an explicit framework

Never order by intuition alone — pick a framework, apply it consistently, and
record the inputs so the ordering is defensible and re-runnable when facts change.

- **RICE** — `(Reach × Impact × Confidence) / Effort`. Best for comparing many
  items on a common scale. Effort comes from [[estimation]].
- **MoSCoW** — Must / Should / Could / Won't. Best for scoping a release.
- **Value vs. effort** — quick 2×2 triage; do high-value/low-effort first.

Record the framework and its inputs on the item so a reviewer sees *why* it
ranks where it does, not just that it does.

**RICE example:**
```
item: Project autosave
reach: 8000 users/mo   impact: 2 (high)   confidence: 80%   effort: 3 pts
RICE = (8000 × 2 × 0.8) / 3 = 4267  → ranks above items scoring lower
```

## Definition of Ready

An item may only move to the top of the queue (pullable by the next stage) when
it is **ready** — otherwise the downstream role stalls or guesses:

- Has a clear user story and testable acceptance criteria (see
  [[requirement_analysis]]).
- Is sized (see [[estimation]]); anything at 13 pts is split first.
- Its dependencies exist or are identified.
- Its priority inputs are recorded.

Items that aren't ready still live in the backlog — just not at the top.

## Grooming

Groom the backlog continuously, not once a quarter:

- **Refine** upcoming items to Ready before they're needed.
- **Re-rank** when new information changes value, effort, or confidence.
- **Split** items too big to reason about or deliver in one slice.
- **Prune** stale items — anything that's sat untouched and no longer serves a
  live goal gets archived or closed, with a reason. A backlog nobody trusts
  because it's full of dead items is worse than a short one.

## Slicing work

Prefer vertical slices that deliver a thin end-to-end increment of user value
over horizontal layers that deliver nothing usable alone. A slice should be
independently valuable, estimable, and testable. If a story can't be finished in
one stage without a giant dependency, it's probably a horizontal slice — reshape
it.

## Keeping it usable

- The backlog holds the ordered *detail*; the [[roadmapping]] roadmap holds the
  thin *direction*. Keep them consistent — top-of-backlog should reflect NOW.
- Maintain it per the [[documentation]] standard so its status and last-updated
  are visible.
- When priorities shift materially, announce it via [[communication]] so
  downstream roles re-plan against the new order rather than the old.
