---
name: test_planning
description: >-
  QA-engineer skill for defining the test strategy for a feature or release — the
  what, why, and how of testing before individual cases are written. Use this
  whenever you decide scope of testing, risk-based priorities, test levels (unit/
  integration/E2E), environments and data, and entry/exit criteria. Consult it
  before writing detailed test cases so testing effort is aimed at the highest
  risks, traces to the PM's acceptance criteria and the architect's NFRs, and has
  clear criteria for when quality is good enough to ship.
---

# Test Planning

Testing everything equally is testing nothing well — time is finite, so the test
strategy's job is to point effort at what's most likely to break and most costly
if it does. A plan grounded in risk and traced to acceptance criteria catches the
defects that matter; an untargeted plan burns effort on trivia and misses the real
risks. This skill sets that strategy before any case is written.

## Anchor to the source-of-truth artifacts

QA validates against upstream artifacts, so start from them:

- [[requirement_analysis]] acceptance criteria — the definition of "works."
- The [[user_flow_design]]/design specs — the states and flows to cover.
- [[nfr_definition]] NFRs — the performance/security/reliability bars to verify.

If acceptance criteria are missing or untestable, that blocks planning — raise it
to the `product-manager` via [[communication]] rather than inventing a bar. QA
tests against acceptance criteria; it does not set them.

## Prioritize by risk

Rank what to test by **likelihood of failure × impact of failure**:

```
- High impact + likely      → test first, most thoroughly
- High impact + unlikely    → cover the critical paths
- Low impact                → light coverage / accept the risk explicitly
```

Money, data-loss, auth, and core-flow paths earn the most scrutiny; cosmetic
edges earn the least. Make the risk calls explicit so coverage is a decision, not
an accident.

## Choose the right test level

Test each thing at the cheapest level that can catch its failures:

- **Unit** — logic and edge cases in isolation (developers own their own; QA fills
  gaps in strategy).
- **Integration** — components/services together, esp. against
  [[api_contract_design]] contracts.
- **E2E** — critical user journeys through the whole [[user_flow_design]] flow.

Avoid pushing everything to slow E2E — a bug catchable in a unit test shouldn't
need a full journey to find.

## Define the plan

```
TEST PLAN: <feature/release>
scope: in / out
risks: <ranked, with the level that covers each>
levels: <what's tested at unit / integration / E2E>
environments & data: <where it runs, what data it needs>
entry criteria: <what must be true before testing starts>
exit criteria: <coverage + severity thresholds to sign off — feeds [[release_validation]]>
```

## Hand off

Publish per the [[documentation]] test-plan structure with traceability to
acceptance criteria. The plan drives [[test_case_design]] (cases),
[[test_automation]] (what to automate), and [[release_validation]] (the exit
bar). Size the effort with [[estimation]] so it can be scheduled.
