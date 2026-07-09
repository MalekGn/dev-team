---
name: nfr_definition
description: >-
  Software-architect skill for defining non-functional requirements — the quality
  attributes the system must meet: performance, scalability, availability,
  reliability, security, and maintainability. Use this whenever you set or revise
  quality targets and constraints that shape architecture. Consult it before
  system-design and tech-stack decisions so NFRs are specific and measurable
  (numbers, not adjectives), traceable to real needs, and testable by QA — vague
  quality goals like "fast" or "scalable" can't be designed or verified against.
---

# NFR Definition

Non-functional requirements are the quality bar the system is judged against —
and unlike features, they shape the *whole* architecture, so they have to be set
before the structure is chosen. Their failure mode is vagueness: "fast",
"scalable", "secure" can't be designed toward or tested, so everyone assumes a
different bar and the gap surfaces in production. This skill turns quality goals
into specific, measurable, verifiable targets.

## Turn adjectives into numbers

Every NFR must be quantified and conditioned, or it's just a hope. Replace each
adjective with a metric, a target, and the condition it holds under:

```
NFR: <quality attribute>
metric: <how it's measured>
target: <the number/threshold>
condition: <load / percentile / environment it applies to>
rationale: <the requirement or risk driving it>
```

**Example:**
```
NFR: API latency
metric: p95 response time for read endpoints
target: < 200 ms
condition: at 500 concurrent users, steady state
rationale: editor autosave must feel instant (PRD Autosave)
```

## Cover the attributes that matter here

Define the ones the product actually needs — don't ceremony-list all of them:

- **Performance** — latency (by percentile), throughput.
- **Scalability** — expected and peak load; growth horizon; scaling approach.
- **Availability / reliability** — uptime target, acceptable error rate, RTO/RPO
  for recovery.
- **Security** — authn/authz expectations, data protection, compliance needs
  (feeds backend [[auth_implementation]]).
- **Maintainability / observability** — what must be logged/monitored so the
  targets can even be measured.

## Trace NFRs to real needs

An NFR with no driver is over-engineering; a missing NFR is a latent outage.
Anchor each to a [[requirement_analysis]] requirement, a known load, or a
concrete risk. If the product needs aren't clear enough to set a target, get them
from the `product-manager` via [[communication]] rather than inventing a number.

## NFRs drive design and get tested

- They are inputs to [[system_design]] and [[tech_stack_selection]] — the
  structure and technology must be chosen to *meet* them, so define them first.
- They are **acceptance criteria for quality**: the `qa-engineer` tests against
  these numbers (load/performance/security testing), so they must be
  objectively verifiable. Record consequential targets in an [[adr_writing]] ADR
  and publish per the [[documentation]] standard.
