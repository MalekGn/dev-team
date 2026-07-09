---
name: tech_stack_selection
description: >-
  Software-architect skill for choosing technologies, frameworks, and patterns.
  Use this whenever you select or evaluate a language, framework, database,
  library, or architectural pattern for the product. Consult it before committing
  to ANY significant technology choice so the decision is driven by requirements
  and constraints, weighs real alternatives against explicit criteria, accounts
  for total cost (team fit, operations, longevity — not just features), and is
  recorded as an ADR the developers build on.
---

# Tech Stack Selection

A technology choice is a long-term liability as much as an asset — the team lives
with it, operates it, hires for it, and pays to migrate off it. Choosing by hype,
familiarity, or a feature checklist ignores the costs that dominate later. This
skill makes stack decisions requirement-driven, comparative, and honest about
total cost — then records them so they're not silently re-litigated.

## Start from requirements and constraints, not preferences

Let the [[requirement_analysis]] requirements and [[nfr_definition]] constraints
set the criteria before you look at options — expected scale, latency, team
skills, operational maturity, licensing, budget, timeline. A choice made before
the criteria are clear is a preference dressed as a decision.

## Evaluate real alternatives against explicit criteria

Never single-source a decision. Put at least two viable options against weighted
criteria so the trade-off is visible:

```
DECISION: <what's being chosen>
criteria (weighted): <fit-to-requirements, team familiarity, ecosystem/maturity,
                      operational cost, performance, licensing/cost, longevity>
options:
  - <A>: strengths / weaknesses vs. each criterion
  - <B>: strengths / weaknesses vs. each criterion
recommendation: <chosen option + the decisive criteria>
```

## Weigh total cost, not just capability

The feature list is the smallest part of the cost. Weigh:

- **Team fit** — can the developers be productive and support it? Exotic tech the
  team can't operate is a hidden tax on every future change.
- **Operability** — deployment, monitoring, upgrades, failure modes.
- **Maturity & ecosystem** — stability, security track record, community/library
  support, hiring pool.
- **Longevity & lock-in** — how painful is it to migrate off later?
- **Boring-by-default** — prefer proven, well-understood tech unless a
  requirement genuinely demands novelty. Novelty is a cost you should choose
  consciously, not by default.

## Match choices to the design

Tech choices must serve the [[system_design]] structure and be implementable
within the [[api_contract_design]] contracts and [[data_modeling]] model — e.g., a
datastore choice follows from the data model's access patterns, not the reverse.

## Handing off

Record every significant choice as an [[adr_writing]] ADR — context, options,
decision, consequences — and publish per the [[documentation]] standard. The
developers implement *within* these choices; if they hit a wall, they raise it via
[[communication]] rather than silently substituting a different technology.
