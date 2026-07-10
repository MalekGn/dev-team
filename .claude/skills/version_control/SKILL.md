---
name: version_control
description: >-
  Shared version-control protocol for the devagent-orch pipeline. Use this whenever
  you interact with git — reading history/diffs/blame to understand existing
  work, creating branches, committing, or opening pull requests. The
  frontend-developer, backend-developer, and qa-engineer have read/write scope
  (they branch, commit, and open PRs); the software-architect has read-only
  scope (inspect history and diffs, never commit). Consult this before ANY git
  action so branches, commits, and PRs are consistently named, scoped, and
  traceable back to the artifact they implement.
---

# Version Control

Git history is the durable record of how the product got built — who changed
what, why, and against which contract. If commits are vague or PRs don't point
back to the spec they implement, the next person (or QA, or the architect
reviewing) has to reverse-engineer intent. This skill keeps the history clean,
scoped, and traceable so a reader can follow any change back to the artifact
that motivated it.

## Know your scope first

Version-control access differs by role. Check yours before acting:

- **read/write** — `frontend-developer`, `backend-developer`, `qa-engineer`.
  You branch, commit, and open PRs. QA writes only test code and tooling, never
  production feature code.
- **read-only** — `software-architect`. You inspect history, diffs, and blame to
  review implementations against your contracts. You do **not** commit or open
  PRs; findings go back as review notes or a `HANDOFF` message.
- **no direct git role** — `product-manager`, `ux-ui-designer`, `orchestrator`.
  Their artifacts live as docs; they don't operate git here.

If an action is outside your scope, decline it and route it per the
[[communication]] `OUT_OF_SCOPE` format.

## One change, one branch, one PR

Each unit of work gets its own branch and its own PR, scoped to a single
contract, spec, or bug. Small, self-contained changes review faster and revert
cleanly. Never commit straight to `main`.

### Branch naming

```
<type>/<short-kebab-summary>
```

`type` is one of: `feat`, `fix`, `test`, `chore`, `refactor`.

**Examples:**
```
feat/project-autosave-endpoint
fix/toolbar-icon-overflow
test/autosave-e2e-coverage
```

## Commit messages

A commit message explains *why* the change exists, not just what the diff shows —
the diff already shows the what. Use Conventional Commits so history is scannable
and the type is machine-readable.

```
<type>(<scope>): <imperative summary>

<body: why this change, and any non-obvious trade-off>

Refs: <upstream artifact path or ticket the change implements>
```

- Keep the summary line ≤ ~72 chars, imperative mood ("add", not "added").
- `scope` is the area touched (e.g., `auth`, `api`).
- Reference the contract/spec/bug the commit implements so history ties back to
  the [[documentation]] artifact that motivated it.
- Commit in logical units — one concern per commit — not one giant end-of-day dump.

**Example:**
```
feat(api): add project autosave endpoint

Implements create/save per the architect contract. Debounced writes are
handled client-side, so the endpoint is a plain idempotent upsert.

Refs: docs/architecture/api-projects.md
```

## Pull requests

A PR is a handoff, so it follows the same "self-contained and traceable" rule as
every other artifact. Write the description with the [[documentation]] PR
guidance; at minimum:

```
## What & why
<what changed and the problem it solves>

## Implements
<contract / spec / PRD / bug it fulfills, by path>

## How verified
<tests added, manual checks, commands run>

## Reviewer notes
<anything to scrutinize, or trade-offs made>
```

- Keep PRs focused — reviewers approve small diffs confidently and rubber-stamp
  large ones.
- Ensure your own tests pass before requesting review (developers: component/
  service tests; QA: the automated suites you own).
- Link the PR back to its upstream artifact so QA and the architect can validate
  against the source of truth.

## Reading history (all read-capable roles)

Before changing or reviewing code, read what's there:

- `git log --oneline -n 20` for recent context.
- `git diff` / `git show <sha>` to inspect a specific change.
- `git blame <file>` to find why a line exists and who owns the context.

The architect works entirely in this read-only mode — inspect the diff against
the contract, then return findings as review notes, never as commits.

## What not to do

- Don't commit to `main` or force-push shared branches.
- Don't bundle unrelated changes into one commit or PR — it hides intent and
  blocks clean reverts.
- Don't commit secrets, credentials, or generated build artifacts.
- Don't commit or push unless the task actually calls for it; when unsure whether
  a change should land, ask via a [[communication]] `QUESTION` first.
