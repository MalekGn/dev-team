---
name: ui_component_development
description: >-
  Frontend-developer skill for building reusable UI components from design specs.
  Use this whenever you create or modify a client-side component: implementing it
  to the design-system spec, handling all its visual/interaction states, defining
  a clean props/API, and making it accessible and reusable. Consult it before
  building ANY component so it faithfully realizes the design-system spec, covers
  every state, and is reusable rather than a one-off — components are the units
  every screen is assembled from.
---

# UI Component Development

Components are the reusable units screens are assembled from, so a well-built one
pays off everywhere and a sloppy one spreads its flaws across the product. The
designer already specified these in the design system; the frontend developer's
job is to realize that spec faithfully and reusably — not to redesign it, and not
to hard-code a single-use variant that fragments the system.

## Realize the design-system spec

Build to the [[design_system_management]] component spec and its
[[visual_design]] tokens — anatomy, variants, and states are defined; implement
them, don't reinvent them. Use design tokens for color/spacing/type rather than
hard-coded values, so the component stays themeable and consistent. If the spec is
missing a case you hit, raise it via [[communication]] to the designer rather than
inventing styling.

## Implement every state

A component isn't done until all its states render correctly:

```
- default / resting
- hover / focus / active     (focus is required for keyboard users)
- disabled
- selected / checked         (where applicable)
- loading / in-progress
- error / invalid
- empty                      (for data-bearing components)
```

Omitting focus or error states is the most common component defect and the
easiest for QA to catch.

## Design a clean component API

A component's props are its contract with the rest of the app — keep it small and
predictable:

- **Minimal, explicit props** — expose what varies; don't leak internals.
- **Sensible defaults** so the common case is trivial to use.
- **Controlled vs. uncontrolled** decided deliberately for inputs.
- **Composition over configuration** — prefer children/slots over a sprawl of
  boolean flags.

## Bake in accessibility

Implement the [[accessibility_design]] semantics from the spec: correct
roles/elements (a real button, not a clickable div), an accessible name, keyboard
operability, visible focus, and state exposed to assistive tech (not just
visually). Accessibility built into the component is inherited by every screen
that uses it.

## Verify and hand off

- Cover the component's states and prop variations with unit tests.
- Check it against the design spec (all states) and accessibility before PR.
- Follow [[frontend_implementation]] for how it fits the larger feature, and
  commit/PR per [[version_control]]. Keep it reusable — if it's turning into a
  one-off, reconsider or flag a new system component to the designer.
