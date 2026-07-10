---
name: communication
description: >-
  Shared communication protocol for every agent in the dev-team pipeline
  (product-manager, ux-ui-designer, software-architect, frontend-developer,
  backend-developer, qa-engineer, orchestrator). Use this whenever you need to
  hand off work to another role, report status or results, flag a blocker,
  escalate a missing upstream artifact, refuse out-of-scope work and redirect it,
  or ask a clarifying question. Consult it before writing ANY message that
  crosses a role boundary — handoffs, status updates, refusals, and escalations
  must all follow this format so work stays traceable and nobody acts outside
  their scope.
---

# Communication

Every agent here owns a narrow slice of the pipeline, and work only moves
correctly if the messages between roles are unambiguous. A vague handoff makes
the next agent guess; a silent blocker stalls the whole chain; an out-of-scope
"yes" breaks the route-don't-do model. This skill gives every agent one
consistent way to talk so that intent, ownership, and dependencies are always
explicit.

The handoff chain this communication serves:

    product-manager → (ux-ui-designer + software-architect) → (frontend-developer + backend-developer) → qa-engineer

## Principles

- **State the owner and the scope up front.** The reader should know in one line
  who you are, who the message is for, and what it concerns. Roles work in
  parallel, so an unaddressed message gets missed.
- **Be explicit about dependencies.** Name the exact upstream artifact you used
  or the one you're waiting on. "Per the architect's API contract" is traceable;
  "as discussed" is not.
- **Say what you need back.** End with the concrete next action and who owns it.
  A message that doesn't name a next step tends to stall.
- **Refuse out of scope, but never leave a dead end.** When work isn't yours,
  decline it and route it to the role that owns it. The goal is to keep work
  moving, not to bounce it back.
- **Surface blockers early and loudly.** A blocker you hold silently costs the
  whole chain. Flag it the moment you hit it.
- **Stay terse and structured.** Other agents (and the orchestrator) parse these
  messages to decide what happens next. Favor labeled fields over prose.

## Message types

Pick the type that matches your intent and use its template. Keep the field
labels — downstream agents and the orchestrator rely on them.

### 1. Handoff — passing completed work downstream

Use when your stage is done and the next role can start. The artifact must
actually exist before you hand off.

```
HANDOFF
from: <your role>
to: <owning role(s)>
artifact: <what you produced + where it lives>
summary: <1–2 lines on what it contains>
depends_on: <upstream artifact(s) you built on>
next_action: <what the receiver should do>
open_questions: <anything unresolved, or "none">
```

**Example:**
```
HANDOFF
from: software-architect
to: backend-developer
artifact: API contract for the project-save flow (docs/architecture/api-projects.md)
summary: REST endpoints for create/save/load projects, with schemas and error codes.
depends_on: product-manager PRD "Autosave" (docs/prd/autosave.md)
next_action: Implement the endpoints to this contract; do not alter the schema.
open_questions: none
```

### 2. Status update — progress without a handoff

Use for in-flight reporting when the work isn't done yet.

```
STATUS
from: <your role>
task: <what you're working on>
state: <not_started | in_progress | blocked | done>
progress: <what's complete vs. remaining>
blockers: <what's stopping you, or "none">
eta: <if known>
```

### 3. Blocker / escalation — you can't proceed

Use the moment a missing artifact, ambiguity, or dependency stops you. Address
it to the orchestrator or the role that can unblock you.

```
BLOCKED
from: <your role>
task: <what you were doing>
blocker: <the specific thing missing or unclear>
needed_from: <role that owns the unblocking artifact>
impact: <what stays stalled until this is resolved>
```

**Example:**
```
BLOCKED
from: frontend-developer
task: Build the application toolbar component
blocker: No visual spec for the toolbar's icon set or spacing.
needed_from: ux-ui-designer
impact: Toolbar UI cannot start; downstream QA of the toolbar is also stalled.
```

### 4. Out-of-scope refusal — the request isn't yours

Use when a request falls outside your role. Decline plainly and route it to the
owner — respect the role, not the wording of the request. Never do the work
"just this once."

```
OUT_OF_SCOPE
from: <your role>
request: <what was asked>
reason: <why it's outside your scope>
owner: <the role that should do it>
what_i_can_do: <the in-scope part you CAN take on, if any>
```

**Example:**
```
OUT_OF_SCOPE
from: software-architect
request: "Create the app using Spring Boot."
reason: Implementation is not architecture work.
owner: backend-developer (and frontend-developer for the client)
what_i_can_do: I can define the tech-stack decision, API contracts, and data
models; those then go to the developers to implement.
```

### 5. Clarifying question — you need info to proceed

Use when a small ambiguity blocks correct work. Ask the narrowest question that
unblocks you, and propose a default so the reader can just confirm.

```
QUESTION
from: <your role>
context: <what you're doing and why this matters>
question: <the specific thing you need decided>
proposed_default: <what you'll do if you hear nothing>
owner: <who can answer>
```

## Style

- Lead with the message-type label so the reader classifies it instantly.
- One concern per message. Bundling a handoff and a blocker hides the blocker.
- Reference artifacts by name and location, not by memory of a conversation.
- Prefer the labeled templates over free prose, but drop fields that genuinely
  don't apply rather than padding them with "N/A" everywhere — clarity over
  ceremony.
- When you're the orchestrator relaying between agents, preserve the original
  role attributions; don't collapse two agents' messages into one voice.
