---
name: test_automation
description: >-
  QA-engineer skill for automating tests — turning test cases into reliable,
  maintainable automated suites at the right level (E2E, integration, regression).
  Use this whenever you write or structure automated test code, decide what to
  automate vs. test manually, or fix flaky tests. Consult it before automating ANY
  suite so the right cases are automated at the cheapest reliable level, tests are
  deterministic (not flaky), and the suite stays maintainable as the product
  changes — QA writes test code and tooling only, never production code.
---

# Test Automation

Automation's value is leverage: a good automated suite verifies the product on
every change, forever, freeing humans for exploratory work. But that value is
fragile — a flaky suite that fails randomly gets ignored, and a brittle one that
breaks on every UI tweak costs more to maintain than it saves. This skill
automates the *right* cases, reliably, and keeps the suite maintainable. QA writes
test code and tooling only — never production feature code.

## Automate what pays off

Not everything should be automated. Favor automation for:

- **Repetitive, stable, high-value** cases — regression suites, critical paths,
  contract checks that run constantly.
- **Deterministic** cases with a clear pass/fail.

Leave to manual/exploratory: one-offs, rapidly-changing UI, and things needing
human judgment (visual polish, UX feel). Automating an unstable target just
creates maintenance debt.

## Automate at the cheapest reliable level

Follow the test-pyramid instinct — prefer the lowest level that can catch the
failure, because lower tests are faster and more stable:

```
- Integration / API   — verify [[api_contract_design]] contracts directly; fast,
                        stable, catches most logic/contract bugs
- E2E (UI)            — reserve for critical [[user_flow_design]] journeys; fewer,
                        because they're slow and the most flake-prone
```

A mountain of slow E2E tests for logic that an API test could cover is a common,
costly anti-pattern.

## Make tests deterministic

Flakiness destroys trust in the suite — hunt it out:

- **No arbitrary sleeps** — wait for explicit conditions/states, not fixed time.
- **Control test data** — each test sets up and tears down its own state; tests
  don't depend on each other or on run order.
- **Isolate external services** — stub/mock third parties ([[integration_development]])
  so results don't depend on someone else's uptime.
- **Assert on stable selectors/contracts**, not brittle DOM structure or copy.

## Keep the suite maintainable

- **One clear reason to fail per test** — a focused assertion that names what
  broke, so a failure is diagnosable at a glance.
- **Reuse setup/helpers** (page objects, fixtures) so a UI/contract change is a
  one-place fix, not a hundred-test rewrite.
- **Fast feedback** — keep the core suite quick enough to run on every change.

## Hand off

Automated suites realize [[test_case_design]] cases and power
[[regression_testing]]. Commit test code per [[version_control]] (QA has
read/write for tests), with the suite runnable in CI. Failures that reveal real
defects become [[bug_reporting]] reports; results feed [[release_validation]].
