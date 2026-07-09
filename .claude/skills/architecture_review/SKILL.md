---
name: architecture_review
description: >-
  Software-architect skill for reviewing implementations and proposed changes
  against the architecture. Use this whenever you check that code, a PR, or a
  design proposal conforms to the system design, API contracts, data model, and
  NFRs — verifying boundaries are respected, contracts are honored, and quality
  targets are met. Consult it before signing off on ANY implementation review so
  findings are specific and actionable — the architect reviews read-only and
  returns notes; it never edits the code or commits.
---

# Architecture Review

Contracts and designs only hold if someone checks that the built system actually
matches them — otherwise the architecture is aspirational and drift creeps in one
PR at a time. Architecture review is that check: it verifies conformance to the
design, contracts, model, and NFRs, and catches erosion early while it's cheap to
fix. Crucially, the architect reviews **read-only** — findings go back as notes,
because implementation belongs to the developers.

## Review read-only, report back

Per [[version_control]], the architect has read-only git scope: inspect the diff,
history, and blame — never commit or edit. Deliver findings as review notes or a
[[communication]] `HANDOFF` to the owning developer. The architect points out
what's off; the developer fixes it.

## Check conformance to the architecture

Review against the artifacts, not personal taste:

```
- Contracts   — does it honor the [[api_contract_design]] shapes, statuses, errors?
- Boundaries  — does it respect [[system_design]] responsibilities, or leak
                across components / reach into another's data?
- Data model  — does it match the [[data_modeling]] entities, keys, integrity?
- NFRs        — does it plausibly meet [[nfr_definition]] targets (perf, security)?
- Standards   — does it follow the agreed patterns and tech choices?
```

A deviation from a contract is a defect even if the code "works" — because the
other side was built to the contract.

## Distinguish must-fix from suggestion

Not every finding is a blocker. Label each so the developer can triage:

- **Blocking** — violates a contract, boundary, or NFR; must change before merge.
- **Recommended** — a real risk or drift worth fixing now.
- **Optional** — a suggestion; the developer's call.

Padding a review with optional nits buries the blocking issues — keep the signal
high.

## Make findings actionable

Each finding names the location, the specific conformance gap, and the standard it
violates — vague disapproval isn't reviewable:

```
FINDING [blocking|recommended|optional]
location: <file:line or component>
issue: <what deviates>
violates: <the contract/boundary/NFR/standard, by name>
suggested direction: <how to bring it back into conformance>
```

## Scope discipline

Review architecture conformance — not code style, product priority, UI, or test
strategy. Route those to their owners via [[communication]]. If the review reveals
the *architecture itself* is wrong (not the implementation), that's a design
change: update the design and record it in an [[adr_writing]] ADR rather than
patching around it in review comments.
