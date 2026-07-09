---
name: roadmapping
description: >-
  Product-manager skill for building and maintaining the product roadmap. Use
  this whenever you sequence initiatives over time, group work into themes or
  milestones, decide what comes now/next/later, or communicate direction and
  trade-offs to stakeholders. Consult it before publishing ANY roadmap so it's
  outcome-oriented, honestly time-framed (not false-precise dates), tied to goals
  and metrics, and clear about what's deliberately deferred.
---

# Roadmapping

A roadmap is a communication tool, not a delivery contract. Its job is to align
everyone on *why* we're building things in a certain order — which outcomes we're
chasing and what we're deliberately choosing not to do yet. A roadmap that reads
as a list of dated features invites false confidence and breaks the moment
reality shifts. This skill keeps the roadmap about outcomes, honestly framed, and
tied to the goals it serves.

## Organize around outcomes, not features

Each roadmap entry should name the **outcome** it targets (the user or business
result), with candidate features as the means. "Reduce time-to-first-edit for new
users" is an outcome; "onboarding wizard" is one bet toward it. Outcomes survive
when a specific feature turns out to be the wrong solution.

## Use horizons, not hard dates

Frame timing in confidence horizons rather than committed calendar dates —
certainty drops the further out you look, and pretending otherwise misleads
stakeholders.

```
NOW    — committed; scoped and in/entering active work.
NEXT   — likely next; shaped but not committed; order may shift.
LATER  — directional; problems we intend to address, not yet shaped.
```

If a stakeholder needs dates, derive a **range** from [[estimation]] sizing and
known capacity for NOW items only — and label it as a forecast, not a promise.

## Every item carries its rationale

An entry is not roadmap-ready until it states why it's placed where it is:

```
## <Outcome / initiative>
- **Horizon:** now | next | later
- **Problem / goal:** <the user or business need it serves>
- **Success metric:** <how we'll know it worked — see [[metric_definition]]>
- **Rough size:** <points/T-shirt from [[estimation]], for NOW/NEXT>
- **Depends on:** <upstream work or decisions>
- **Why now (or why deferred):** <the sequencing rationale>
```

## Sequencing principles

- **Value and risk first.** Pull high-value or high-uncertainty work earlier —
  learning early is cheaper than learning late.
- **Respect the handoff chain.** Nothing enters NOW that lacks its upstream
  artifacts (requirements → design/architecture). Sequence so upstream work
  lands before the stage that depends on it.
- **Limit work in NOW.** A roadmap that commits to everything commits to nothing;
  a short NOW is a real priority signal.
- **Make deferrals explicit.** State what's in LATER or cut, so "not now" is a
  visible decision rather than a silent gap.

## Keeping it alive

- Re-sequence when goals, metrics, or estimates change — a stale roadmap is a
  liability. Communicate material shifts via [[communication]].
- Publish it per the [[documentation]] standard (owner, status, last-updated) so
  readers know how current it is.
- The roadmap sets direction; the ordered, groomed detail lives in the
  [[backlog_management]] backlog. Keep the roadmap thin and the backlog specific.
