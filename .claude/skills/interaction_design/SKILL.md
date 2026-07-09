---
name: interaction_design
description: >-
  UX/UI-designer skill for designing how the interface behaves over time —
  interaction patterns, transitions, feedback, and micro-behaviors. Use this
  whenever you specify what happens when a user acts: hover/press/focus feedback,
  loading and progress, transitions between states, optimistic vs. confirmed
  updates, gestures, and error recovery behavior. Consult it before finalizing ANY
  interactive spec so behavior is defined explicitly for the frontend developer
  instead of being improvised at implementation time.
---

# Interaction Design

Wireframes and visual specs describe screens at rest; interaction design
describes what happens *between* those states — the feedback, timing, and
transitions that make an interface feel responsive and predictable. Leave this
unspecified and the frontend developer invents it, so behavior varies screen to
screen and QA has nothing concrete to test. This skill pins the behavior down.

## Behavior follows structure

Interaction design builds on a settled [[user_flow_design]] flow and
[[wireframing]] layout — it defines the *motion and feedback* connecting the
states those already established, not new structure. Reference the flow's states
by name so the developer maps behavior to the exact screens.

## Specify feedback for every action

Users need to know their action registered. For each interactive element, define:

```
- Trigger            — click / tap / hover / focus / key / gesture
- Immediate feedback — what changes at once (press state, ripple, focus ring)
- In-progress        — loading/disabled/skeleton while work happens
- Result             — success confirmation or error + recovery
- Reversibility      — can it be undone/cancelled, and how
```

Silence after an action reads as "broken" — every trigger gets acknowledged.

## Choose an update model deliberately

For actions that hit the server (via the architect's contracts), decide and state:

- **Optimistic** — reflect the change immediately, reconcile on response, roll
  back on failure. Feels fast; specify the rollback behavior.
- **Confirmed** — show progress, apply only on success. Safer for
  costly/irreversible actions.

Whichever you pick, define what the user sees on latency and on failure — the
error path is part of the interaction, not an exception.

## Motion with purpose

Use transitions to explain change, not to decorate:

- Motion should show cause/relationship (where something came from/went) or mask
  latency — not draw attention to itself.
- Use [[design_system_management]] motion tokens (standard durations/easings) so
  timing is consistent, not hand-tuned per screen.
- Honor reduced-motion preferences per [[accessibility_design]]; motion must
  never be the *only* way state is conveyed.

## Handing off

Fold behavior into the [[documentation]] design spec alongside the wireframe and
visual spec, so the `frontend-developer` gets structure, style, and behavior as
one coherent package, and the `qa-engineer` can test the interaction states.
Interaction design answers *what happens when the user acts*.
