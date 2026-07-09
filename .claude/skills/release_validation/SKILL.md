---
name: release_validation
description: >-
  QA-engineer skill for the final quality gate — deciding whether a build is ready
  to ship. Use this whenever you validate a release: confirming acceptance
  criteria and NFRs are met, running the regression and smoke suites, checking
  open-defect severity against exit criteria, and giving a clear go/no-go sign-off.
  Consult it before ANY release decision so sign-off is an evidence-based judgment
  against pre-agreed exit criteria — not a gut feeling — and the residual risk is
  stated explicitly.
---

# Release Validation

Release validation is the last gate before users are exposed to the build, and its
integrity depends on one thing: the decision is made against **pre-agreed exit
criteria with evidence**, not a deadline-pressured gut call. A rubber-stamp
sign-off defeats the entire pipeline's discipline; a clear-eyed one, honest about
residual risk, is what lets the team ship with confidence. This skill makes the
go/no-go call defensible.

## Validate against the agreed bar

Sign-off checks the build against the criteria set upstream — not against what
feels done:

```
- Acceptance criteria — every [[requirement_analysis]] criterion in scope, verified
- NFRs                — [[nfr_definition]] targets met (perf, security, reliability)
- Regression          — [[regression_testing]] suite passing; old behavior intact
- Smoke               — critical paths work on the actual release build/environment
- Open defects        — checked against the [[test_planning]] exit criteria
```

If exit criteria were never defined, that's a gap — get them from
[[test_planning]] and the `product-manager` before validating, per
[[communication]]. QA verifies the bar; it doesn't lower it under pressure.

## Judge defects against exit criteria, not zero

Shipping requires zero *blocking* defects, not zero defects — perfection is not
the bar, and pretending it is either never ships or hides the real risks. Apply
the exit criteria:

- **Critical/high open defects** → typically no-go (or an explicit, owned waiver).
- **Medium/low** → ship with them *documented* as known issues, if within
  criteria.
- Severity is QA's read ([[bug_reporting]]); the ship-with-known-issues *decision*
  belongs to the `product-manager` — QA surfaces, PM decides.

## Give a clear, evidence-based verdict

A sign-off is a decision, so state it unambiguously with the evidence behind it:

```
RELEASE SIGN-OFF: <build/version>
verdict: GO | NO-GO | GO WITH CONDITIONS
criteria met: <acceptance / NFR / regression / smoke — status of each>
open defects: <count by severity, blockers named>
known issues: <what ships unfixed, and why it's acceptable>
residual risk: <what could still go wrong, and any mitigation/rollback>
conditions: <if conditional — what must hold, e.g., a hotfix ready>
```

Never a bare "looks good." Name what was verified and what risk remains — an
honest NO-GO or a stated residual risk protects the team far more than an
optimistic GO.

## Own the gate, stay in scope

- The verdict is QA's professional judgment against the evidence; don't let
  schedule pressure convert a NO-GO into a GO — flag the conflict via
  [[communication]] and let the `product-manager` own any risk-acceptance
  decision explicitly.
- Record the sign-off per the [[documentation]] standard so the decision and its
  basis are traceable after release.
