---
name: design_system_management
description: >-
  UX/UI-designer skill for building and maintaining the design system — the
  shared library of tokens and components every screen is built from. Use this
  whenever you define, extend, or govern design tokens (color, type, spacing) and
  reusable component specs, decide whether a new pattern belongs in the system, or
  keep the system consistent as the product grows. Consult it before introducing
  ANY new component or token so the system stays the single source of truth
  instead of fragmenting into one-offs.
---

# Design System Management

The design system is the single source of truth for how the product looks and
behaves at the component level. Its whole value is leverage: define a button once,
and every screen and every developer gets a consistent, accessible one for free.
That leverage evaporates the moment one-off components and ad-hoc values
proliferate — then the "system" is just a folder. This skill keeps it the
authoritative, reused foundation.

## Tokens are the foundation

Everything visual traces to tokens, so a change propagates instead of being hunted
down per screen:

```
- Color tokens        — semantic roles (surface, text, primary, danger, border…)
- Typography tokens   — a named type scale
- Spacing tokens      — one consistent scale (e.g., 4/8-based)
- Radius / elevation  — a small fixed set
- Motion tokens       — standard durations/easings (feeds [[interaction_design]])
```

[[visual_design]] and [[wireframing]] must consume these, not invent parallel
values. If a needed token doesn't exist, add it to the system — don't inline it.

## Components are specified, not just drawn

A system component carries a complete spec so it's reused correctly:

```
COMPONENT: <name>
purpose: <when to use it — and when NOT to>
anatomy: <parts, and which are optional>
variants: <e.g., primary/secondary/ghost>
states: <default/hover/focus/active/disabled/error, per [[visual_design]]>
tokens: <the tokens it uses>
a11y: <roles, labels, focus behavior — per [[accessibility_design]]>
```

The "when NOT to use it" line prevents misuse as much as the rest of the spec.

## Governing additions

Guard the system against sprawl. Before adding a component or token, ask:

- Does an existing component (or a variant of one) already serve? Prefer
  extending over adding.
- Will this be reused across screens, or is it a genuine one-off? One-offs stay
  local; reusable patterns get promoted into the system.
- Does it fit the existing token language, or does it demand a new token? A new
  token is a system-level decision, not a per-screen convenience.

## Consistency and change

- **One name, one meaning.** Don't let two tokens or components mean the same
  thing — that's how systems fragment.
- **Version changes deliberately.** A token change ripples everywhere; treat it
  per the [[documentation]] standard (status, last-updated) and announce
  breaking changes via [[communication]] so the `frontend-developer` can adapt.
- **Deprecate, don't orphan.** When a pattern is replaced, mark the old one
  deprecated with its successor, so usage migrates instead of lingering.
