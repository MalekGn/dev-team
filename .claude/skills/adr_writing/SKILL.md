---
name: adr_writing
description: >-
  Software-architect skill for writing Architecture Decision Records — short
  documents that capture a significant technical decision, why it was made, and
  its consequences. Use this whenever a consequential, hard-to-reverse choice is
  made (structure, tech stack, data model, contract style, key trade-off).
  Consult it before finalizing ANY such decision so the reasoning is recorded at
  the moment of choosing — the context, the alternatives, and the trade-offs —
  so future readers understand why, not just what, and don't relitigate settled
  ground.
---

# ADR Writing

Architecture is a chain of decisions, and the reasoning behind them evaporates
fast — six months later nobody remembers why the datastore was chosen, so someone
"fixes" it and reintroduces the problem it solved. An ADR freezes the *why* at the
moment of the decision: the forces, the options weighed, and the trade-offs
accepted. It's cheap insurance against relitigating settled ground and against
silent, context-free reversals.

## What deserves an ADR

Record decisions that are **significant and costly to reverse** — not every small
call:

- Structural choices ([[system_design]] boundaries, sync vs. async).
- Technology selections ([[tech_stack_selection]]).
- Data-model and [[api_contract_design]] conventions with wide blast radius.
- [[nfr_definition]] targets that shape the architecture.
- Any decision where a future reader would reasonably ask "why did we do it this
  way?"

If reversing it later would be cheap and local, it probably doesn't need an ADR.

## Structure

Keep ADRs short and immutable-by-default — one decision each:

```
# ADR-<NNN>: <short title of the decision>

- **Status:** proposed | accepted | superseded by ADR-<NNN>
- **Date:** <date>
- **Deciders:** <role(s)>

## Context
<the forces at play — requirements, constraints, the problem creating pressure>

## Decision
<what we chose, stated plainly>

## Alternatives considered
<the real options, and why each was not chosen>

## Consequences
<what this makes easier and harder; trade-offs accepted; follow-ups/risks>
```

## Write it well

- **Capture the context honestly.** The value is in the forces and constraints at
  the time — a decision that looks wrong later often was right for its context.
- **Show the alternatives.** An ADR with no rejected options isn't a decision
  record, it's an announcement. The roads not taken are what stop relitigation.
- **Be honest about consequences.** Name the downsides you accepted. Pretending a
  choice is all upside destroys the record's credibility.
- **One decision per ADR**, numbered sequentially, so each is citable.

## Lifecycle: append, don't rewrite

ADRs are a historical record. Don't edit an accepted ADR to reflect a new
decision — write a **new** ADR that supersedes it, and update the old one's status
to point forward. The trail of superseded decisions is itself valuable context.

## Handing off

Store ADRs at a stable path per the [[documentation]] standard so any role can
trace a decision. When an ADR changes what developers must do, flag it via
[[communication]]; the developers build within accepted ADRs, and the architect
enforces them during [[architecture_review]].
