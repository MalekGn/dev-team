---
name: system_design
description: >-
  Software-architect skill for designing the overall shape of the system —
  components, service boundaries, responsibilities, and how they interact. Use
  this whenever you define or revise high-level structure: decomposing the system
  into services/modules, drawing boundaries, choosing communication styles
  (sync/async), and describing data and control flow. Consult it before ANY
  detailed contract, data-model, or tech-stack work so the structure is
  deliberate, requirement-driven, and gives developers clear boundaries to build
  within — the architect designs structure only and never implements.
---

# System Design

System design is where the product's shape is decided: what the major pieces are,
who owns what, and how they talk. Get the boundaries right and teams work in
parallel with clean seams; get them wrong and every feature smears across
components and every change ripples. This skill defines that structure
deliberately, from requirements — and stops at the boundary of *design*, because
implementation belongs to the developers.

## Design from requirements and constraints

Structure serves the product, so start from the [[requirement_analysis]]
requirements and the non-functional needs (see [[nfr_definition]]) — expected
scale, latency, reliability. If those inputs are missing, request them via a
[[communication]] `BLOCKED`/`QUESTION` rather than designing against assumptions.

## Decompose along real boundaries

Split the system where responsibilities and change-rates actually diverge, not by
arbitrary layers:

- **High cohesion, low coupling** — each component owns one clear responsibility;
  crossings between them are few and explicit.
- **Boundaries follow the domain and the data** — a component owns its data;
  others reach it through its interface, never its storage.
- **Design for change** — put the volatile behind stable interfaces so churn
  stays local.

## Describe structure explicitly

Since diagrams here are textual, describe them precisely:

```
- Components/services  — name + single responsibility of each
- Boundaries           — what each owns; what it explicitly does NOT
- Interactions         — who calls whom, sync vs. async, and why
- Data flow            — how data moves through for the key scenarios
- Trust boundaries     — where auth/validation happens (feeds backend auth)
```

Walk the primary user scenarios through the structure to prove it actually
supports them end-to-end.

## Sync vs. async, and coupling

Choose communication styles on purpose: synchronous for request/response the user
waits on; asynchronous/evented for work that can decouple in time or must not
block. Every remote call is a failure point — note where retries, timeouts, and
fallbacks belong so the developers implement them.

## Handing off

System design produces the frame the rest of architecture fills in:
[[api_contract_design]] for the interfaces, [[data_modeling]] for the data,
[[tech_stack_selection]] for the technology, and [[adr_writing]] to record the
consequential choices. Package per the [[documentation]] standard and hand
implementation to the developers — **design the structure; never write the
feature code.**
