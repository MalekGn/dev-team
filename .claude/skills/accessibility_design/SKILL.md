---
name: accessibility_design
description: >-
  UX/UI-designer skill for designing accessible experiences from the start. Use
  this whenever you need to ensure a flow, wireframe, component, or visual spec
  works for everyone — color contrast, keyboard and focus order, screen-reader
  semantics, target sizes, motion sensitivity, and clear labeling. Consult it
  before finalizing ANY design spec so accessibility is designed in (cheap) rather
  than retrofitted after implementation (expensive and incomplete).
---

# Accessibility Design

Accessibility is a design property, not a QA afterthought. Decisions made here —
contrast, focus order, what's conveyed by color, whether a control has a real
label — are cheap to get right in a spec and painful to bolt on after the
frontend developer has built to a spec that ignored them. This skill bakes
accessibility into the design so the whole downstream chain inherits it.

## Design to WCAG, at least AA

Treat WCAG 2.1 AA as the baseline for every spec:

- **Contrast** — 4.5:1 for body text, 3:1 for large text and essential UI/icons.
  Check as you pick colors in [[visual_design]], not after.
- **Color is never the only signal** — pair color with text, icon, or pattern, so
  meaning survives color blindness and grayscale.
- **Target size** — interactive targets large enough to hit reliably (aim ~44px);
  spacing so adjacent controls aren't mis-tapped.

## Keyboard and focus are part of the flow

Every interaction must work without a mouse. In the [[user_flow_design]] and
[[interaction_design]] specs, define:

- **Focus order** — logical, following reading/flow order.
- **Visible focus** — a clear focus indicator on every interactive element.
- **No traps** — the user can always move focus onward and escape overlays.
- **Shortcuts/gestures** have a keyboard-accessible equivalent.

## Give the screen reader something to say

Specify semantics so assistive tech conveys structure and meaning:

```
- Roles / semantics    — heading levels, landmarks, lists, buttons vs. links
- Names / labels       — every control and input has an accessible name
- State announcements  — loading, error, selected, expanded are exposed, not just visual
- Alt text intent      — what images/icons should convey (or mark decorative)
- Live regions         — where dynamic updates should be announced
```

Fold these into the [[design_system_management]] component specs so accessibility
is inherited by reuse, not re-specified per screen.

## Respect motion and cognition

- Honor reduced-motion preferences; don't rely on motion to convey state.
- Avoid content that flashes; keep essential animation subtle and optional.
- Keep language and error messages plain and specific — clarity is accessibility.

## Handing off and verifying

Include an **accessibility notes** section in every [[documentation]] design spec
so the `frontend-developer` implements the semantics and the `qa-engineer` has
concrete, testable criteria. Accessibility requirements are acceptance criteria —
verifiable, not aspirational; flag gaps via [[communication]] rather than shipping
them silently.
