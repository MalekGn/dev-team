---
name: requirement_analysis
description: >-
  Product-manager skill for turning a raw request, idea, or problem into clear,
  testable requirements. Use this whenever you must analyze what's actually being
  asked — elicit the real need behind a feature request, disambiguate vague
  asks, separate problem from proposed solution, define user stories, and write
  acceptance criteria QA can validate against. Consult it before writing ANY PRD
  or user story so requirements capture the underlying need, are unambiguous, and
  hand off cleanly to design, architecture, and QA.
---

# Requirement Analysis

Everything downstream is built against requirements — design interprets them,
architecture is shaped by them, developers implement them, QA validates against
them. A requirement that conflates a problem with one proposed solution, or that
can't be objectively verified, propagates that flaw through the entire pipeline.
This skill turns a raw ask into requirements that capture the real need and are
testable.

## Start from the problem, not the solution

Requests usually arrive as solutions ("add a dark mode toggle"). Your first job
is to recover the problem underneath ("users editing at night are strained by a
bright UI"). The problem is stable and admits many solutions; the proposed
solution may be wrong. Record the problem, the affected user, and the desired
outcome before any solution language.

## Interrogate every requirement

Before writing anything down, pressure-test the ask:

- **Who** is this for, and what are they trying to accomplish?
- **Why** now — what's the underlying need or pain?
- **What does success look like**, observably?
- **What's explicitly out of scope?**
- **What's assumed** that might not hold?
- **What are the edge cases** — empty, error, concurrent, offline states?

If answers are missing and block correct work, ask via a [[communication]]
`QUESTION` with a proposed default rather than guessing.

## User story format

Express requirements as user stories so they stay user-centered and sized for
the backlog.

```
As a <type of user>,
I want <capability>,
so that <outcome / why>.
```

The `so that` clause is not optional — it's the problem statement that lets
design and architecture choose the right solution.

## Acceptance criteria

Every story carries acceptance criteria that are **objectively verifiable** —
QA validates against these, so "works well" or "is fast" won't do. Prefer the
Given/When/Then form for behavior:

```
Given <precondition>,
when <action>,
then <observable result>.
```

Cover the happy path, the important edge cases, and error states. If you can't
write a criterion someone could pass/fail without judgment, the requirement is
still ambiguous — refine it.

**Example:**
```
Story: As a returning user, I want my project to autosave, so that I never lose work.

Acceptance criteria:
- Given an open project with unsaved edits, when 3s pass with no further edit,
  then changes persist and a "saved" indicator appears.
- Given a save request that fails, when the error returns, then the user sees a
  retry affordance and no edits are lost locally.
- Given two edits within 3s, when the timer fires, then only one save occurs.
```

## Quality checklist

A requirement is ready to hand off when it is:

- **Unambiguous** — one reasonable interpretation.
- **Testable** — QA can objectively verify it.
- **Necessary** — traces to a real user problem or goal.
- **Feasible-agnostic** — states the need, not the implementation (leave
  "how" to architecture and the developers).
- **Scoped** — in/out boundaries are explicit.

## Handing off

Requirements feed the whole downstream chain, so package them per the
[[documentation]] PRD structure and hand off per [[communication]] to both the
`ux-ui-designer` (for flows/specs) and the `software-architect` (for contracts).
Keep the analysis about *what and why*; the *how* belongs to those roles.
Size stories with [[estimation]] so they can be sequenced in the [[backlog_management]] backlog.
