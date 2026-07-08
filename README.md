# dev-team

A role-scoped AI agent team for a mobile/web app editor company. This repository
defines a fixed set of specialist agents and the operating rules that coordinate
them, so that product work flows through a disciplined, single-responsibility
pipeline instead of an ad-hoc, do-everything assistant.

## Purpose

Building a mobile/web app editor product involves distinct disciplines —
product, design, architecture, implementation, and quality. This project encodes
those disciplines as separate agents with exclusive scopes and a mandatory
handoff chain. The goals are:

- Keep each stage of work owned by the right specialist.
- Prevent scope creep (no coding before requirements, no building before
  architecture, etc.).
- Make handoffs and dependencies explicit and enforceable.

## Target Users

- Teams and operators using this repository to run product development through a
  structured, route-don't-do agent model.
- Product, design, architecture, engineering, and QA stakeholders who need clear
  ownership boundaries and predictable handoffs.

## How It Works

Every request enters through the **orchestrator**, which classifies it and routes
it to the owning specialist(s). No specialist work is performed outside its owning
agent, and no stage may start before its upstream artifacts exist.

**Handoff chain:**

```
product-manager → (ux-ui-designer + software-architect) → (frontend-developer + backend-developer) → qa-engineer
```

## The Agent Team

- **orchestrator** — single entry point; routes work, enforces scope, sequences
  handoffs. Performs no specialist work itself.
- **product-manager** — product vision, requirements, roadmap, backlog,
  priorities, and acceptance criteria.
- **ux-ui-designer** — user flows, wireframes, visual/UI specs, and design system.
- **software-architect** — system design, tech stack, API contracts, data models,
  and ADRs (defines architecture only; does not implement).
- **frontend-developer** — client-side implementation per designer specs and
  architect contracts.
- **backend-developer** — server-side implementation per architect contracts.
- **qa-engineer** — test strategy, test cases, automation, bug reports, and
  release sign-off.

The full operating rules are defined in [`CLAUDE.md`](./CLAUDE.md), and each
agent's exclusive scope is defined in [`.claude/agents/`](./.claude/agents/).

## Roadmap / Status

**Current status:** Foundation stage. The repository currently contains the
role-scoped agent team and the operating rules (route-don't-do dispatch model and
handoff chain). No product application has been built yet.

**Planned / upcoming:**

- Product definition — PRDs, backlog, and prioritized roadmap for the app editor
  (owned by product-manager).
- Design — user flows, wireframes, and design system (owned by ux-ui-designer).
- Architecture — system design, tech stack, API contracts, and data models
  (owned by software-architect).
- Implementation — client and server (owned by frontend-developer and
  backend-developer).
- Quality — test strategy and release readiness (owned by qa-engineer).

## Architecture

_Coming soon._ Architecture, tech-stack decisions, API contracts, and data models
are pending the software-architect stage and do not exist yet.

## Setup & Usage

_Coming soon._ Setup, build, and run instructions will be added once the
architecture and implementation stages produce the corresponding artifacts
(pending the software-architect and developer stages).
