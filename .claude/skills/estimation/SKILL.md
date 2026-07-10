---
name: estimation
description: >-
  Shared estimation protocol for the devagent-orch pipeline (product-manager,
  software-architect, frontend-developer, backend-developer, qa-engineer). Use
  this whenever you size a piece of work — sizing backlog items or a roadmap,
  weighing the effort of architecture options, estimating implementation of a
  feature, or estimating test effort for a release. Consult it before giving ANY
  effort or time estimate so every estimate carries the same units, states its
  confidence and assumptions, and is comparable across roles instead of being an
  unqualified guess.
---

# Estimation

Estimates drive sequencing, scope trade-offs, and commitments across this whole
pipeline — the PM prioritizes with them, the architect chooses between options
with them, developers and QA plan with them. A bare number ("about 3 days") with
no assumptions or confidence attached is worse than useless: it looks precise
while hiding all the risk. This skill makes every estimate carry the same units,
its confidence, and the assumptions it rests on, so estimates mean the same thing
no matter which role produces them.

## Core rules

- **Estimate size and uncertainty, not a false-precise date.** Effort you can
  reason about; a calendar date depends on capacity and interruptions you don't
  control. Size the work; let planning turn size into schedule.
- **Always attach confidence.** An estimate without a confidence level implies
  certainty you don't have. Low confidence is a signal to spike or decompose,
  not a failure.
- **Make assumptions explicit.** Every estimate rests on assumptions ("the API
  contract is stable", "no new design needed"). Written down, they can be
  checked; unwritten, they silently break the estimate.
- **Decompose big or fuzzy work.** Anything above your top size bucket, or that
  you can't reason about confidently, gets broken into parts you can. A single
  huge estimate hides where the real risk is.
- **Estimate your own scope only.** Size the work your role owns; flag
  dependencies on other roles rather than estimating their part for them.

## Units: relative size, not raw hours

Estimate in **story points** on a modified Fibonacci scale. Points capture
effort + complexity + uncertainty together and stay stable even when who does
the work changes.

| Points | Meaning |
|--------|---------|
| **1**  | Trivial; well understood; touches one place. |
| **2**  | Small; understood; a little coordination. |
| **3**  | Moderate; some unknowns or a few moving parts. |
| **5**  | Large; several parts or notable uncertainty. |
| **8**  | Very large; many parts or significant unknowns — consider splitting. |
| **13** | Too big to estimate reliably — **decompose before committing**. |

If a stakeholder needs calendar time, convert points to a **range** at planning
time using known capacity — never quote a single hardened date off a point value.

## Confidence

Tag every estimate with one:

- **High** — done something nearly identical; few unknowns.
- **Medium** — understood in shape, but real unknowns remain.
- **Low** — significant unknowns; the estimate could move a lot. Pair a Low with
  a proposed spike or a decomposition to raise confidence.

## Report an estimate like this

Keep it compact and structured so the reader (often the PM sequencing work, or
the orchestrator) can use it directly.

```
ESTIMATE
from: <your role>
item: <what's being sized + link to the artifact>
size: <points>
confidence: high | medium | low
assumptions: <what must hold for this to be accurate>
excludes: <related work NOT covered by this estimate>
dependencies: <what you're waiting on from other roles>
risks: <what could make it bigger>
```

**Example:**
```
ESTIMATE
from: backend-developer
item: Project autosave endpoint (docs/architecture/api-projects.md)
size: 3
confidence: medium
assumptions: API contract is final; reuse existing persistence layer.
excludes: Client-side debounce logic (frontend-developer owns that).
dependencies: None once the contract is approved.
risks: If conflict-resolution is required, this jumps to a 5.
```

## How each role applies it

The units and format are shared; what you size differs by role:

- **product-manager** — size backlog items and epics to sequence the roadmap and
  make scope trade-offs. Push anything at 13 back to the owning role to
  decompose before it enters a committed sprint.
- **software-architect** — attach relative effort to design *options* so the PM
  can weigh cost against value; estimate the architecture/spec work itself, not
  the downstream implementation.
- **frontend-developer / backend-developer** — size implementation of the
  contract/spec you'll build, excluding the other's half and flagging shared
  dependencies.
- **qa-engineer** — size test strategy, authoring, and automation effort against
  the acceptance criteria; call out where thin specs inflate the estimate.

## Keep estimates honest

- Re-estimate when assumptions change — an estimate is a snapshot, not a
  contract. Say so via a [[communication]] `STATUS` update when a number moves.
- Don't pad silently to feel safe; express the risk in `confidence` and `risks`
  instead, where it's visible and can be discussed.
- Distinguish estimate from commitment. You estimate effort; sequencing and
  commitment are the PM's and orchestrator's call.
