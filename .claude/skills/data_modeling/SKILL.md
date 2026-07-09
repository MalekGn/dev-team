---
name: data_modeling
description: >-
  Software-architect skill for designing the data model — entities, their
  attributes, relationships, and the rules that keep data correct. Use this
  whenever you define or revise how data is structured and persisted: entities
  and fields, keys and relationships, constraints and integrity rules,
  normalization vs. denormalization, and indexing/access considerations. Consult
  it before backend developers build persistence so the model is consistent with
  the API contracts and enforces integrity — the architect designs the model; the
  backend developer implements the storage.
---

# Data Modeling

The data model is the most expensive thing to get wrong: code is rewritten in an
afternoon, but a bad schema drags migrations, data cleanups, and years of
workarounds behind it. A model that doesn't enforce its own integrity lets bad
data accumulate silently until something downstream breaks. This skill designs a
model that's correct, consistent with the contracts, and durable — and leaves the
implementation to the backend developer.

## Model the domain, aligned to the contracts

Entities come from the [[requirement_analysis]] domain and must line up with the
[[api_contract_design]] schemas — the same concepts, named the same way. A
mismatch between the contract's "project" and the model's "document" becomes a
translation bug in every endpoint. Design the model as the source of truth the
contracts expose.

## Specify each entity fully

```
ENTITY: <name>
purpose: <what real-world thing it represents>
attributes: <field : type : required? : constraints/defaults>
identity: <primary key / natural key>
relationships: <to which entities, cardinality (1:1, 1:N, N:M), ownership>
integrity: <uniqueness, referential rules, cascade/restrict on delete>
lifecycle: <created/updated/soft-delete; any state field + allowed transitions>
```

## Let the model enforce correctness

Push invariants into the schema wherever possible — a constraint the database
enforces can't be bypassed by a buggy code path:

- **Keys and uniqueness** for identity and to prevent duplicates.
- **Referential integrity** so relationships can't dangle; decide cascade vs.
  restrict deliberately.
- **Non-null and value constraints** for fields that must always be valid.

Application-level rules the backend developer must enforce (because the store
can't) should be called out explicitly so they're not forgotten.

## Normalize, then denormalize on purpose

Default to a normalized model — one fact in one place avoids update anomalies.
Denormalize only for a measured access-pattern need (a hot read path), and when
you do, name what keeps the duplicated data in sync. Note the key access patterns
so the backend developer knows where **indexes** matter.

## Design for change

- Prefer additive evolution; plan how the model migrates without downtime or data
  loss, and note it for the backend developer.
- Avoid destructive assumptions (hard deletes where history matters — consider
  soft-delete/audit needs from requirements).
- Record consequential modeling trade-offs in an [[adr_writing]] ADR.

## Handing off

Publish the model per the [[documentation]] standard alongside the
[[api_contract_design]] contracts. The `backend-developer` implements persistence
and migrations to this model; changes are announced via [[communication]] so
contracts and code stay aligned.
