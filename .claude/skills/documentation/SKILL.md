---
name: documentation
description: >-
  Shared documentation standard for every producing role in the dev-team
  pipeline (product-manager, ux-ui-designer, software-architect,
  frontend-developer, backend-developer, qa-engineer). Use this whenever you
  write a durable artifact that another role will read and act on — PRDs, user
  stories, design specs, redline notes, ADRs, API contracts, technical
  standards, code/README docs, PR descriptions, test plans, or bug reports.
  Consult it before writing ANY document that outlives the current task so the
  artifact is self-contained, findable, versioned, and usable by the downstream
  role without a live conversation.
---

# Documentation

Work in this pipeline moves through written artifacts, not conversations. The
architect's contract is read by developers days later; the PM's acceptance
criteria are validated by QA at the end of the chain. If a document assumes
context the reader doesn't have, the handoff silently fails. This skill sets one
standard so every artifact is self-contained, findable, and actionable by the
next role — no matter which agent wrote it.

## What good documentation does here

- **Stands on its own.** A reader with no memory of the originating conversation
  can act on it. State the context, don't assume it.
- **Names its audience and its dependencies.** Say who it's for and which
  upstream artifact it builds on, so the reader can trace the chain backward.
- **Is decision-complete.** It answers the questions the downstream role will
  actually ask. A spec that omits error states forces the developer to guess.
- **Is findable and stable.** It lives at a predictable path and carries a
  status so readers know whether to trust it yet.

## Every artifact starts with this header

Whatever the document type, open it with a short metadata block. It costs four
lines and saves the reader from guessing whether the doc is current, who owns
it, and what it depends on.

```
# <Title>

- **Owner:** <role that wrote it>
- **Status:** draft | in_review | approved | superseded
- **Depends on:** <upstream artifact(s) + path, or "none">
- **Last updated:** <date>
```

Then the body, structured for the document type below.

## Where artifacts live

Keep artifacts at predictable paths so any role can find them without asking:

- `docs/prd/` — PRDs, user stories, acceptance criteria (product-manager)
- `docs/design/` — flows, wireframe specs, redline notes, design tokens (ux-ui-designer)
- `docs/architecture/` — ADRs, API contracts, data models, standards (software-architect)
- `docs/qa/` — test plans, test cases, bug reports (qa-engineer)
- Code docs and PR descriptions live with the code (frontend-developer, backend-developer)

## Structures by document type

Use the skeleton for the artifact you're writing. These are starting points, not
cages — add sections the reader needs, drop ones that don't apply.

### PRD (product-manager)
```
## Problem / Opportunity
## Goals & success metrics
## User stories
## Acceptance criteria      (testable; QA validates against these)
## Scope: in / out
## Open questions
```

### Design spec (ux-ui-designer)
```
## User flow
## Layout / wireframe description
## Components & states       (default, hover, empty, error, loading)
## Design tokens             (color, spacing, typography referenced by name)
## Accessibility notes
## Redlines / measurements
```

### ADR (software-architect)
```
## Context                   (forces at play)
## Decision                  (what we chose)
## Alternatives considered
## Consequences              (trade-offs, follow-ups)
## Status                    (proposed / accepted / superseded)
```

### API contract (software-architect)
```
## Endpoint / operation
## Request                   (method, path, params, body schema)
## Response                  (schemas per status code)
## Errors                    (codes + meanings)
## Auth & constraints
## Examples                  (concrete request/response pairs)
```

### Test plan (qa-engineer)
```
## Scope & what's under test
## Traceability              (which acceptance criteria each case covers)
## Test cases                (steps, expected result)
## Environments / data
## Entry & exit criteria
```

### Bug report (qa-engineer)
```
## Summary
## Severity / priority
## Steps to reproduce
## Expected vs. actual
## Environment
## Evidence                  (logs, screenshots referenced by path)
```

### Code & PR docs (frontend-developer, backend-developer)
- Document the *why*, not the *what* — the code shows what; comments explain
  intent, constraints, and non-obvious trade-offs.
- A PR description states what changed, which contract/spec it implements (by
  path), how it was verified, and anything a reviewer should scrutinize.
- Match the surrounding code's comment density and idiom; don't over-annotate.

## Writing style

- **Concrete over abstract.** "Returns 409 on a duplicate slug" beats "handles
  conflicts gracefully."
- **Reference, don't restate.** Link the upstream artifact by path instead of
  copying it; copies drift out of sync.
- **Tables and lists over paragraphs** for anything a reader will scan or check
  off — acceptance criteria, endpoints, test cases.
- **One source of truth per fact.** If two docs would state the same thing, one
  owns it and the other links to it.
- **Mark uncertainty explicitly.** An open question flagged as such is useful; a
  guess presented as fact is a landmine for the downstream role.
