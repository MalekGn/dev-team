---
name: visual_design
description: >-
  UX/UI-designer skill for the visual layer — applying color, typography,
  spacing, and hierarchy to settled wireframes. Use this whenever you specify how
  a screen or component should look: type scale, color usage, spacing/layout
  grid, elevation, and visual states. Consult it before producing ANY visual spec
  so styling is expressed as reusable design tokens (not one-off values), stays
  consistent with the design system, meets contrast requirements, and gives the
  frontend developer exact redlines to build from.
---

# Visual Design

Visual design turns settled structure into a finished, consistent look. Done as
tokens and system rules, it scales across the product; done as one-off hex values
sprinkled per screen, it drifts into inconsistency the moment a second designer or
a new screen appears. This skill expresses the visual layer as reusable decisions
the frontend developer can implement exactly.

## Style structure, don't restructure

Visual design comes after [[wireframing]] has settled layout and hierarchy. Your
job is to make that hierarchy *read* through type, color, and space — not to
re-argue what goes where. If styling reveals a structural problem, raise it back
to the wireframe rather than papering over it with visual tricks.

## Express everything as tokens

Never hand the developer raw values scattered per screen. Define the visual
language once as [[design_system_management]] tokens and reference them:

```
- Color        — semantic roles (surface, text, primary, danger…), not raw hex per use
- Typography   — a type scale (sizes, weights, line-height) applied by role
- Spacing      — a spacing scale (e.g., 4/8-based) used for all gaps and padding
- Radius/elevation — a small fixed set, not arbitrary per element
```

Tokens make the design themeable and consistent; ad-hoc values guarantee drift.
For anything involving data or charts, follow the project's dataviz guidance for
palettes rather than inventing chart colors here.

## Meet contrast and legibility up front

Accessibility is cheaper designed-in than retrofitted. Check text and essential
UI against WCAG contrast (4.5:1 body text, 3:1 large text/UI) as you choose
colors, and never encode meaning in color alone. Coordinate with
[[accessibility_design]] for the full picture.

## Specify visual states

Style every state the wireframe defined — default, hover, focus, active,
disabled, selected, error — not just the resting state. A button spec that omits
focus and disabled forces the developer to guess, and guesses drift from the
system.

## Redlines for handoff

Give the frontend developer buildable precision:

```
COMPONENT: <name>
tokens: <color/type/spacing tokens used, by name>
measurements: <padding, gaps, sizes — as scale steps, not magic numbers>
states: <default / hover / focus / active / disabled / error styling>
notes: <anything non-obvious>
```

Deliver per the [[documentation]] design-spec structure, referencing the
[[wireframing]] screens and feeding the `frontend-developer`. Styling answers
*how it looks*; behavior over time is [[interaction_design]].
