---
name: regression_testing
description: >-
  QA-engineer skill for ensuring new changes don't break existing, working
  functionality. Use this whenever you guard against regressions: selecting which
  existing tests to re-run for a change, maintaining the regression suite, adding
  a test for every fixed bug, and scoping regression effort by risk. Consult it
  before signing off on ANY change so previously-working behavior is re-verified —
  new features that quietly break old ones are among the most damaging and
  embarrassing defects.
---

# Regression Testing

The most damaging bugs are often the ones in features that *used* to work — a
change ripples somewhere unexpected, nobody re-checked it, and it ships broken.
Regression testing is the guard against that: re-verifying existing behavior still
holds after a change. Done well, it lets the team change code confidently; skipped,
every new feature is a gamble on the old ones. This skill keeps the safety net
effective and affordable.

## Every fix gets a regression test

The single highest-value habit: when a [[bug_reporting]] defect is fixed, add an
automated test that reproduces it. That test fails on the old bug and passes on
the fix — so the bug can never silently return. A bug that recurs because nobody
captured it is a preventable, credibility-costing failure.

## Scope regression by risk and blast radius

Re-running everything on every change is often too slow; running nothing is
reckless. Scope by what the change can plausibly affect:

```
- Directly changed area        — full re-test
- Shared code / dependencies   — test what consumes it
- Critical paths (auth, data,  — always re-verify, regardless of the change
  payments, core flows)
- Unrelated, isolated areas    — lighter or skip, deliberately
```

Use the [[system_design]] boundaries to reason about blast radius — a change
inside one component with clean seams ripples less than one touching shared code.

## Automate the regression suite

Regression is repetitive and stable — exactly what [[test_automation]] is for.
Maintain a regression suite that runs on every change (in CI), so re-verification
is automatic rather than a manual chore that gets skipped under deadline. Manual
regression is reserved for what can't be reliably automated.

## Keep the suite healthy

A regression suite decays if untended — prune and maintain it:

- **Fix or remove flaky tests fast** — a suite that cries wolf gets ignored, which
  defeats the entire purpose.
- **Retire truly obsolete tests** when behavior is intentionally changed (confirm
  the change is intended, via [[communication]], before deleting a failing test —
  a real regression can masquerade as an "outdated" test).
- **Keep it fast enough to actually run** every change; a suite too slow to run is
  a suite that doesn't protect you.

## Fit the release

Regression results are a required input to [[release_validation]] sign-off —
"new work passes" isn't enough; "old work still passes" is half the bar. Commit
suite changes per [[version_control]] and report regressions found as
[[bug_reporting]] defects.
