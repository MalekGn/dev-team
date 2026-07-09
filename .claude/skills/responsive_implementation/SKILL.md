---
name: responsive_implementation
description: >-
  Frontend-developer skill for implementing responsive, adaptive layouts across
  screen sizes and devices. Use this whenever UI must work on more than one
  viewport: fluid layouts, breakpoints, reflow/stacking, touch vs. pointer input,
  and adapting the design spec's responsive intent to real screens. Consult it
  before building ANY layout for a multi-device product so it adapts gracefully
  from mobile to desktop instead of breaking or being retrofitted screen by
  screen.
---

# Responsive Implementation

This is a mobile/web app editor — the same UI has to work on a phone and a wide
desktop, so responsiveness isn't a finishing touch, it's structural. Layouts that
assume one width break the moment the viewport changes, and retrofitting
responsiveness screen by screen afterward is far more work than building fluid
from the start. This skill implements the designer's responsive intent so the UI
adapts cleanly across devices.

## Build on the design's responsive intent

The [[wireframing]] spec states what should reflow, stack, hide, or resize at
different sizes — implement that intent, don't guess it. If the spec is silent on
how a screen behaves at a given size, ask the designer via [[communication]]
rather than inventing a breakpoint behavior that may clash with the design.

## Fluid first, breakpoints for real shifts

Start from layouts that flex naturally (flexible grids, relative units,
constraints) so most adaptation happens without any breakpoint. Add breakpoints
only where the layout genuinely needs to *change* — reflowing from multi-column to
stacked, moving navigation — not to hard-code a few fixed widths.

```
- Fluid by default    — relative units, flex/grid, max-width, min/max sizing
- Breakpoints         — only where structure must change, matching the spec
- Content-driven      — let content and container drive breakpoints, not specific
                        device models (which change constantly)
```

## Design for touch and pointer

A multi-device UI is used by both finger and mouse:

- **Touch targets** large enough to hit (~44px) and spaced to avoid mis-taps, per
  [[accessibility_design]].
- **No hover-only affordances** — anything reachable on hover must be reachable by
  tap/focus too, since touch has no hover.
- **Respect input and viewport** — safe areas, on-screen keyboards, orientation.

## Verify on the range, not one screen

- Check the real breakpoints and the sizes *between* them (the awkward
  in-between widths are where layouts break), not just phone and desktop extremes.
- Verify text scaling and zoom don't break layout — an accessibility requirement.
- Cover every state ([[frontend_implementation]]) at the small size too; error and
  empty states also have to reflow.

## Fit the larger feature

Responsive behavior is one facet of the component and feature work — coordinate
with [[ui_component_development]] (components must themselves be responsive) and
watch [[client_performance]] (don't ship desktop-weight assets to phones).
Commit/PR per [[version_control]], noting responsive behavior verified.
