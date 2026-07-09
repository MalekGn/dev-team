---
name: wireframing
description: >-
  UX/UI-designer skill for laying out screens as low-to-mid fidelity wireframes.
  Use this whenever you define what goes on a screen and where — content
  hierarchy, layout regions, component placement, and the per-screen states
  (default, empty, loading, error) — before visual styling. Consult it before ANY
  visual-design pass so the structure is settled first: grounded in the user
  flow, complete across states, and specific enough for a frontend developer to
  build against.
---

# Wireframing

A wireframe settles *structure* — what's on the screen, its priority, and where
it sits — deliberately before color and polish, so those decisions aren't
argued while layout is still moving. A wireframe that shows only the full,
happy-path screen leaves the developer to invent the loading and empty states;
one without a stated hierarchy gets styled into visual noise. This skill gets the
bones right and complete first.

## Build on the flow

Each wireframe realizes a screen from a [[user_flow_design]] flow. Before laying
anything out, know which flow step this screen is, what the user is trying to do
here, and which states the flow says it must have. Don't wireframe screens the
flow doesn't call for.

## Establish hierarchy first

Decide what matters most on the screen and make the layout say so. The primary
action or content gets prominence; secondary options recede. If everything looks
equally important, nothing is. State the intended hierarchy explicitly — the
frontend developer needs to know what dominates.

## Specify each screen completely

For every screen, describe:

```
- Purpose            — the one thing the user does here
- Layout regions     — header / nav / content / actions, and their arrangement
- Components         — what sits in each region (by generic type)
- Content priority   — primary vs. secondary emphasis
- States             — default, empty, loading, error, and any flow branches
- Responsive intent  — what reflows/stacks on small screens (hand to
                       [[responsive_implementation]] via specs)
```

## Fidelity: enough to build, not more

Stay low-to-mid fidelity — boxes, labels, and real-ish content, not final visual
styling. The goal is an unambiguous structure the [[visual_design]] pass can
style and a developer can implement. Use placeholder-but-plausible content, not
"lorem ipsum" for critical labels — real labels expose length and hierarchy
problems early.

## Reference the design system

Lay out with existing [[design_system_management]] components wherever they fit,
naming them so the frontend developer reuses rather than rebuilds. Only propose a
new component when nothing in the system serves — and flag it for the system.

## Handing off

Deliver wireframes per the [[documentation]] design-spec structure. They feed
[[visual_design]] (styling), [[interaction_design]] (behavior), and
[[accessibility_design]] (structure/semantics), and ultimately the
`frontend-developer`. The wireframe answers *what and where*; styling and
behavior come next.
