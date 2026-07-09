---
name: database_access
description: >-
  Backend-developer skill for implementing data persistence and access. Use this
  whenever you read or write the database: implementing queries and persistence
  to the architect's data model, using transactions, preventing injection,
  handling migrations, and keeping queries efficient. Consult it before writing
  ANY data-access code so persistence respects the model's integrity rules, is
  safe against injection, and doesn't introduce N+1 or unindexed-scan performance
  problems.
---

# Database Access

The database is the system's durable source of truth, so data-access code carries
outsized weight: a correctness bug here corrupts data permanently, and a
performance bug here (an N+1 loop, an unindexed scan) degrades everything above
it. The [[data_modeling]] model already defines the structure and integrity
rules; this skill implements access that respects them, stays safe, and stays
fast.

## Implement to the data model

Persist and query against the [[data_modeling]] entities, keys, and relationships
exactly — same names, same constraints. Don't reshape the schema to make a query
convenient; if the model genuinely doesn't support a needed access pattern, that's
an architect decision — raise it via [[communication]], don't add a rogue column
or table.

## Correctness: transactions and integrity

- **Use transactions** for any unit of work that must be all-or-nothing —
  partial writes are how data gets corrupted. Keep transactions as short as
  correctness allows to avoid lock contention.
- **Respect and rely on model constraints** — let uniqueness/foreign-key/not-null
  constraints enforce integrity rather than hoping application code always does.
- **Handle concurrency** — expect concurrent writers; use the model's strategy
  (optimistic versioning or locking) so lost-update and race bugs don't slip in.

## Safety: never build queries from raw input

- **Parameterize every query** — use bound parameters/prepared statements or the
  ORM's safe interface. String-concatenating user input into SQL is the classic
  injection hole; never do it.
- **Least privilege** — access with the narrowest DB permissions the service
  needs.
- **Don't leak** — DB errors returned to callers use the contract's error
  envelope, never raw driver messages.

## Performance: the usual traps

Most database slowness is a handful of patterns — avoid them by default:

```
- N+1 queries      — loading a list then querying per-row; batch/join instead
- Unindexed reads  — filtering/sorting on unindexed columns; index the access
                     paths the model flagged (confirm with the architect)
- Over-fetching    — SELECT * / loading unused columns/rows; fetch what you need
- Unbounded results — always paginate large collections per the contract
```

Measure against the [[nfr_definition]] targets rather than guessing — profile the
actual query when a path is slow.

## Migrations

Evolve the schema through versioned, reversible migrations, never ad-hoc manual
changes. Prefer additive, backward-compatible changes so deploys don't break
running code; for destructive changes, plan the data preservation. Follow the
[[data_modeling]] migration guidance and commit migrations per [[version_control]].

## Verify

Test persistence logic — including transaction rollback and constraint violations
— per [[backend_implementation]]. Data-access bugs are expensive; the error and
concurrency paths are exactly what to test.
