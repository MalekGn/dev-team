---
name: user_flow_design
description: >-
  UX/UI-designer skill for mapping the paths a user takes to accomplish a goal.
  Use this whenever you design or revise a user flow — the sequence of screens,
  decisions, and states from an entry point to a completed task, including happy
  path, branches, and error/empty/edge states. Consult it before ANY wireframing
  so the flow is grounded in the PM's requirements, covers the states developers
  and QA will need, and hands off cleanly to visual design.
---

# User Flow Design

A flow is the skeleton every screen hangs on. Design screens before the flow and
you get pretty dead-ends; nail the flow first and the wireframes almost write
themselves. A flow that only covers the happy path guarantees the developer
improvises the empty and error states and QA finds the gaps late. This skill maps
the whole path — including the states nobody likes to draw — before any pixels.

## Start from the goal and the requirement

Every flow serves a user goal drawn from a [[requirement_analysis]] user story.
State the actor, their goal, and the trigger that starts the flow before drawing
steps. If the requirement is ambiguous about what "done" means, resolve it via a
[[communication]] `QUESTION` before designing around a guess.

## Map the whole path, not just the happy one

For each flow, capture:

```
- Entry point(s)        — how the user arrives
- Steps                 — each screen/action toward the goal
- Decision points       — branches, with the condition for each
- Success state         — what "done" looks like
- Empty states          — first-run / no-data
- Error & recovery      — what fails, what the user sees, how they recover
- Exits                 — abandon, back, cancel
```

The non-happy states are where handoffs break — treat empty and error states as
first-class, not afterthoughts.

## Represent it clearly

Describe flows as a numbered sequence with explicit branches, or as a node/arrow
description. Keep each step atomic (one user intention). Name screens
consistently so the [[wireframing]] and [[interaction_design]] work can reference
them unambiguously.

**Example:**
```
Flow: New user creates first project
1. Empty dashboard (empty state) → [Create project] CTA
2. Project setup screen → name + template
   - branch: no template chosen → default blank template
3. App opens with starter content (success)
   - error: creation fails → inline error + retry, user stays on setup
Exits: Cancel on step 2 → back to empty dashboard
```

## Keep flows honest

- **One goal per flow.** If it forks into two goals, it's two flows.
- **No orphan states.** Every screen has a way in and a way out.
- **Match reality.** Only include branches the requirement actually implies;
  don't invent scope — flag missing requirements back to the `product-manager`.

## Handing off

Package flows per the [[documentation]] design-spec structure and hand them to
[[wireframing]] and [[interaction_design]] as the backbone. The flow defines
*what states exist and how they connect*; layout and micro-behavior come next.
