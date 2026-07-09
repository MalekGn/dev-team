---
name: bug_reporting
description: >-
  QA-engineer skill for writing clear, actionable bug reports and tracking them to
  closure. Use this whenever you document a defect: reproduction steps, expected
  vs. actual, severity/priority, evidence, and routing to the owning role.
  Consult it before filing ANY bug so it's reproducible, correctly triaged, and
  routed to the right owner — a bug a developer can't reproduce or understand
  can't be fixed, and a mis-triaged one steals attention from what matters.
---

# Bug Reporting

A bug report is a handoff to whoever will fix it, and its whole value is enabling
that fix — which means it must be **reproducible** and **understandable**. A report
that says "it's broken" wastes a round-trip; a developer who can't reproduce it
closes it as "works for me" and the defect ships. This skill writes reports that
get bugs fixed, triaged so the important ones get attention first.

## Make it reproducible — the one non-negotiable

If the developer can't reproduce it, they can't fix it. Give them everything
needed to see the failure themselves:

```
BUG: <short, specific summary of what's wrong>
severity: <critical | high | medium | low>
environment: <build/version, device/browser, OS, config>
preconditions: <state/data/account needed>
steps to reproduce: <exact, numbered, minimal>
expected: <what should happen — cite the acceptance criterion/spec>
actual: <what happens instead>
evidence: <logs, screenshots, video, network trace — referenced by path>
```

Reduce steps to the **minimal** reproduction — strip the incidental so the real
trigger is obvious. Reproduce it yourself before filing.

## Separate severity from priority

They're different axes, and conflating them mis-schedules fixes:

- **Severity** = technical impact if it occurs (crash/data-loss = critical;
  cosmetic = low). QA sets this from evidence.
- **Priority** = how soon to fix it, given severity *and* business context. That's
  the `product-manager`'s call — QA proposes, PM decides.

Ground severity in observed impact, not annoyance, so the ranking stays credible.

## Describe behavior, against the source of truth

- State **expected vs. actual** in terms of the [[requirement_analysis]] acceptance
  criterion or the design/[[api_contract_design]] spec it violates — "actual: 500,
  contract specifies 409" is actionable; "actual: it broke" is not.
- Report the **symptom, not a guessed cause** — diagnosis is the developer's job;
  a wrong guessed cause misleads them. Include evidence and let it point.
- **One bug per report** so each can be triaged, fixed, and verified independently.

## Route to the owner and track to closure

- Route by where the defect lives, per [[communication]]: client → `frontend-developer`,
  server → `backend-developer`, spec/contract gap → `software-architect`,
  requirement/criteria gap → `product-manager`.
- Track the lifecycle (open → in progress → fixed → **verified/closed**). A "fixed"
  bug isn't closed until QA re-tests and confirms — and adds a
  [[regression_testing]] case so it can't silently return.
- File and maintain per the [[documentation]] bug-report structure.
