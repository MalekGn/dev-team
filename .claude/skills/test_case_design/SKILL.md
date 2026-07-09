---
name: test_case_design
description: >-
  QA-engineer skill for designing concrete, verifiable test cases from acceptance
  criteria and specs. Use this whenever you write test cases: deriving them from
  acceptance criteria, covering happy path, edge cases, and error/negative paths,
  and using techniques like boundary and equivalence analysis. Consult it before
  writing ANY test case so each is specific, reproducible, traced to the criterion
  it verifies, and covers the failure paths — not just the happy path everyone
  remembers to check.
---

# Test Case Design

A test case is only useful if it's specific enough that anyone can run it and get
the same pass/fail — and if the *set* of cases actually covers where bugs hide. The
common failure is testing only the happy path: the demo works, but the empty
input, the boundary value, and the error response — where most real defects live —
go unchecked. This skill designs cases that are reproducible and cover the paths
that matter.

## Derive cases from acceptance criteria

Each test case traces to a [[requirement_analysis]] acceptance criterion or a spec
state — that's what makes coverage measurable and stops testing from wandering.
The Given/When/Then acceptance criteria map almost directly to cases. If a
criterion is too vague to turn into a pass/fail case, it's not testable — send it
back to the `product-manager` via [[communication]].

## Write each case to be reproducible

```
CASE: <id> — <what it verifies>
verifies: <acceptance criterion / spec state / NFR>
preconditions: <state/data required>
steps: <exact, ordered actions>
test data: <specific inputs>
expected: <the one observable, unambiguous result>
```

"Expected: works correctly" is not a test case. The expected result must be
something a runner can objectively confirm without judgment.

## Cover more than the happy path

Systematically design for the paths bugs hide in:

- **Happy path** — the criterion's main success case.
- **Negative/error paths** — invalid input, unauthorized access, the contract's
  error responses ([[api_contract_design]]) — verify it fails *correctly*.
- **Edge/empty states** — empty, first-run, maximum, concurrent, offline (the
  states the [[user_flow_design]] and design specs define).

## Use technique to cut case count, not coverage

Testing every input is impossible; techniques get near-full coverage with few
cases:

- **Equivalence partitioning** — one case per class of inputs treated the same
  (one valid, one invalid per class), instead of dozens of near-identical inputs.
- **Boundary analysis** — test at and just past the edges (0, 1, max, max+1);
  bugs cluster at boundaries far more than in the middle.
- **Decision tables** — for logic with combinations of conditions, cover the
  meaningful combinations rather than all of them.

## Hand off

Organize cases per the [[documentation]] test-plan structure with traceability, so
gaps are visible. Cases feed [[test_automation]] (which get automated) and are run
during [[regression_testing]] and [[release_validation]]. Defects found become
[[bug_reporting]] reports.
