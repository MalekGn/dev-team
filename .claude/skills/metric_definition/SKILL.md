---
name: metric_definition
description: >-
  Product-manager skill for defining the metrics that measure product success.
  Use this whenever you set KPIs, choose a north-star metric, define success
  metrics for a feature or roadmap item, or add guardrail metrics that protect
  against a metric being gamed. Consult it before attaching ANY metric to a PRD,
  roadmap entry, or acceptance discussion so metrics are specific, measurable,
  tied to a real outcome, and paired with guardrails — not vanity numbers.
---

# Metric Definition

Metrics decide whether the work was worth it and steer what the team optimizes
next. A badly chosen metric is actively harmful: a vanity number ("total
signups") looks like progress while hiding whether anyone got value, and a metric
without a guardrail invites gaming (drive "time in app" up by making the app
confusing). This skill makes every metric specific, tied to a real outcome, and
protected against perverse incentives.

## Measure outcomes, not activity

Prefer metrics that capture whether users got value over metrics that just count
motion. "Weekly users who complete an edit" beats "page views"; the first is an
outcome, the second is activity that may signal nothing. Ask: if this number goes
up, are users actually better off?

## Define each metric completely

A metric named without a definition is ambiguous — three people will compute it
three ways. Specify it fully:

```
METRIC
name: <what it's called>
question: <the user/business question it answers>
definition: <exact formula — numerator / denominator, event, window>
segment: <who it's measured over — all users? new? a cohort?>
target: <current baseline → goal, with timeframe>
guardrail_for: <if this is a guardrail, what it protects>
source: <where the data comes from, once instrumented>
```

**Example:**
```
METRIC
name: Activation rate
question: Do new users reach first value quickly?
definition: % of new signups who complete ≥1 project edit within 24h of signup
segment: New users, weekly cohort
target: 34% → 50% within Q3
guardrail_for: —
source: product analytics (edit_completed event)
```

## Structure: one primary, supported by inputs and guardrails

- **North-star / primary** — the single metric that best captures the core value
  delivered. One per product or major area; more than one and the team pulls in
  different directions.
- **Input metrics** — the levers that move the primary; these are what teams
  actually act on week to week.
- **Guardrail metrics** — the things that must *not* get worse while you chase
  the primary (e.g., error rate, latency, churn, support load). Every offensive
  metric needs at least one guardrail, or you'll optimize it into a problem.

## Good metrics are

- **Specific** — one unambiguous formula.
- **Measurable** — instrumentable from real events, not guesswork.
- **Actionable** — the team can influence it; a metric nobody can move is a
  scoreboard, not a tool.
- **Resistant to gaming** — paired with guardrails so the easy way to move it
  is also the right way.
- **Time-bound** — carries a baseline, a target, and a window.

## How metrics connect to the pipeline

- Attach success metrics to [[requirement_analysis]] requirements and
  [[roadmapping]] roadmap items — a feature with no defined metric can't be
  judged a success or failure later.
- Metrics are not acceptance criteria: acceptance criteria say the feature
  *works* (QA validates them); metrics say the feature *mattered* (measured in
  production over time). Keep the two distinct.
- Publish metric definitions per the [[documentation]] standard so everyone
  computes them the same way, and flag changes via [[communication]].
