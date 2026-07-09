---
name: stakeholder_communication
description: >-
  Product-manager skill for communicating with stakeholders — the audience-facing
  counterpart to the shared communication protocol. Use this whenever you write
  for people outside the build pipeline: status and progress updates, explaining a
  prioritization or trade-off decision, saying no to a request, sharing the
  roadmap, or aligning stakeholders on scope. Consult it before ANY
  stakeholder-facing message so it leads with what they care about, is honest
  about trade-offs and risk, and turns product decisions into shared
  understanding.
---

# Stakeholder Communication

The shared [[communication]] skill governs terse, structured messages *between
agents in the pipeline*. This skill is different: it's for communicating outward
to **stakeholders** — leadership, customers, other teams — who don't live in the
backlog and don't want field-labeled templates. Their questions are "what's
happening, why, and what does it mean for me?" Answering those clearly is how a
PM builds the trust that lets the team keep making hard prioritization calls.

## Lead with what the stakeholder cares about

Different audiences need different things — open with theirs:

- **Leadership** — outcomes, risks, and decisions needed. Not task lists.
- **Customers / users** — the benefit and when, in their language, not the org's.
- **Other teams** — what changes for them and what you need from them.

Put the headline first. Stakeholders skim; bury the point and it's missed.

## Be honest about trade-offs and risk

Credibility is the PM's only real currency. Sugar-coating a slip or hiding a risk
buys a day and costs the trust you need for the next hard call. State reality,
then the plan.

- Frame status as **outcome + confidence + risk**, not just "on track."
- When something slips or is cut, say so plainly, give the reason, and state the
  mitigation or the trade-off accepted.
- Distinguish a forecast from a commitment (carry over the [[estimation]]
  discipline — ranges and confidence, not false-precise dates).

## Saying no

Most of a PM's job is choosing what *not* to do now. A good "no" preserves the
relationship by showing the reasoning, not by hedging into a soft yes:

```
- Acknowledge the request and the need behind it.
- Explain the trade-off: what it would displace and why that's worse.
- Offer the alternative — a later horizon, a smaller version, or the real owner.
```

Anchor the reasoning in the [[roadmapping]] roadmap and
[[backlog_management]] priority framework so "no" reads as a transparent
decision, not a personal veto.

## Status update template

```
## <Initiative> — <period>
- **Headline:** <the one thing to know>
- **Progress:** <what shipped / advanced toward the outcome>
- **Metrics:** <movement on the success metric, if any — see [[metric_definition]]>
- **Risks / blockers:** <honest, with mitigation>
- **Decisions needed:** <what you need from this audience, by when>
- **Next:** <what's coming, with confidence>
```

## Principles

- **Translate, don't dump.** Turn pipeline detail into what it *means* for the
  reader; internal status labels and story IDs rarely belong here.
- **Match the medium to the stakes.** A one-line async note for routine
  progress; a written, reasoned brief for a big trade-off or a "no."
- **Close the loop.** If a stakeholder input changed a decision, tell them — it's
  how you keep them engaged and honest inputs coming.
- **One source of truth.** Point to the [[documentation]] roadmap/PRD rather than
  restating it; keep the message about interpretation and decisions.
