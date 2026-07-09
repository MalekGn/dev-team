---
name: frontend_implementation
description: >-
  Frontend-developer skill for implementing client-side features — the general
  discipline of turning designer specs and architect contracts into working,
  maintainable client code. Use this whenever you build or modify client-side
  functionality: wiring UI to data, structuring client modules, handling client
  logic and validation, and integrating the sub-skills (components, state, API
  integration, responsiveness, performance). Consult it before writing ANY client
  code so implementation faithfully follows the design spec and API contract
  rather than improvising either.
---

# Frontend Implementation

The frontend developer sits at the receiving end of two upstream contracts — the
designer's spec and the architect's API contract — and the core discipline is
*fidelity*: build exactly what those specify, no more and no less. Improvising UI
the designer didn't spec, or a request shape the contract didn't define, breaks
the parallel-work model and surfaces as an integration bug. This skill keeps
implementation faithful and maintainable, and coordinates the specialized
frontend sub-skills.

## Build to the spec and the contract

Before writing code, have both inputs in hand:

- The [[wireframing]]/[[visual_design]]/[[interaction_design]] design spec — what
  it looks like and how it behaves, across all states.
- The [[api_contract_design]] contract — the exact data shapes you send/receive.

If either is missing or ambiguous, stop and raise a [[communication]]
`BLOCKED`/`QUESTION` — do not invent the missing design or API. You implement the
client per specs and contracts; you don't define UI or architecture.

## Implement every state, not just the happy one

The design spec defines default, empty, loading, error, and disabled states —
build them all. A screen that only handles loaded-with-data is half-built and will
fail QA. Map each state in the spec to real UI.

## Structure for maintainability

- **Compose from components** (see [[ui_component_development]]) — reuse the
  design system rather than rebuilding.
- **Keep logic out of the view** — presentation renders; data-fetching and rules
  live in clearly separated units, so both stay testable.
- **Match the codebase.** Follow existing patterns, naming, and idioms; read
  neighboring code before adding new shapes.

## Coordinate the sub-skills

Frontend work draws on the specialized skills — reach for them explicitly:

- [[ui_component_development]] — building the visual components.
- [[state_management]] — client state and data flow.
- [[api_integration_client]] — talking to the backend per contract.
- [[responsive_implementation]] — behavior across screen sizes.
- [[client_performance]] — keeping it fast.

## Verify and hand off

- Write component-level unit tests for your own code (the `qa-engineer` owns
  overall test strategy, not your unit tests).
- Verify against the design spec's states and the contract before opening a PR.
- Commit and PR per [[version_control]], with the description referencing the
  spec and contract you implemented per [[documentation]].
- Stay in scope: no server code, no architecture decisions, no redesigning the UI
  — route those via [[communication]].
