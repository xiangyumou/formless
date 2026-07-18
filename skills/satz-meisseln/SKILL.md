---
name: satz-meisseln
description: Use for implementation planning after a Formless specification has been approved and the work requires a multi-task handoff or the user explicitly requests a written implementation plan with fixed structure and context pointers
---

# Satz meisseln

## Overview

Chisel an approved specification into a durable implementation plan that
another engineer or model can execute without the conversation that shaped it.

Write implementation plans for another engineer or model to execute with little
conversation context. Preserve decisions that require judgment; leave
mechanical work to the implementer.

Plans are for coordination, not ceremony. An obvious localized change that can
be implemented safely in less time than it takes to describe should be made
directly unless the user explicitly requested a plan-only deliverable.

## Scope Gate

Before writing a plan, classify the task:

- **Direct change:** localized, reversible, root cause and implementation are
  clear, and no architectural decision is needed. Implement it directly and run
  proportionate verification.
- **Planned change:** spans meaningful boundaries, has dependencies or interface
  decisions, carries migration or compatibility risk, or will be handed to a
  model without the current context. Require an approved spec, then write a
  plan.
- **Unclear or unapproved change:** important decisions are missing or the spec
  is not approved. Return to `formless:worte-fangen`; do not turn uncertainty
  into invented plan steps.

## Planning For Handoff

Assume the implementer is capable but has no conversation history. Include:

- target files or components when known, or a bounded discovery area when not
- intended behavior and acceptance criteria
- consequential decisions and constraints that must not be re-decided
- interfaces between tasks, with exact contracts where integration depends on them
- proportionate verification evidence, with exact commands only when non-obvious
- escalation conditions for facts that would invalidate the chosen direction

Start with enough background for the implementer to understand the system,
where this change belongs, and why the chosen approach fits. Add a context map
that points to the authoritative files for current behavior, interfaces,
repository conventions, and verification. Do not reproduce every detail from
those files.

At task level, include only the context specific to that deliverable: why the
task exists, what prior work it depends on, and which files to read first. Do
not repeat the full project background in every task.

Resolve choices that materially affect behavior, architecture, data ownership,
public interfaces, compatibility, security, or cross-task integration. When
several viable choices exist, select one and record the reason; obtain user
input first when the choice belongs to the user.

Leave routine engineering judgment to the implementer: local naming, helper
decomposition, edit order, and implementation details that follow clearly from
repository conventions. Show exact code or signatures only when correctness or
an inter-task contract depends on that exact shape. Do not inventory every
delegated detail; state implementation freedom only where a boundary could
otherwise be mistaken for a prescribed mechanism.

The plan has the right resolution when the implementer does not need to make a
product or architectural decision, but still has room to implement the chosen
direction idiomatically. Specify outcomes and guardrails, not keystrokes.

## Task Boundaries

A task is one coherent deliverable worth handing to a fresh implementer and
reviewing on its own.

Group the implementation, its appropriate verification, and closely related
configuration or documentation into the same task. Writing a test, running it,
changing code, running checks, and committing are execution details, not
separate tasks or plan steps.

Split only when at least one is true:

- the pieces produce independently useful behavior
- they touch distinct components with a clear interface
- they can be implemented and reviewed independently
- separation materially reduces context or risk

Avoid plans with many tiny tasks. A small feature may be one task. A complex
feature should have as few tasks as its real dependency structure allows.

## Verification Strategy

Choose verification based on what could realistically fail and what evidence
would detect that failure. A production change does not automatically require a
new test.

Add a test only when all of these are true:

1. It protects behavior or an invariant that matters beyond this patch.
2. A plausible future regression would make it fail for a useful reason.
3. The assertion can remain stable when implementation details change.
4. Its confidence is worth its maintenance and execution cost.

If those conditions are not met, use the most direct relevant evidence already
available: existing tests, static checks, a build, a focused smoke check, or
inspection of the actual result. Record why that evidence is sufficient when
the choice would not be obvious to the implementer.

Never create a test whose main purpose is to record that this particular edit
was made. Tests are durable behavior checks, not a duplicate change log.

## Plan Process

1. Read the approved spec and verify that its status is `Approved` and its open
   questions are resolved.
2. Inspect the source files named by the spec and discover any additional
   authoritative files required for implementation.
3. Write the draft plan to
   `docs/formless/plans/YYYY-MM-DD-<topic>.md` using the exact format below.
4. Self-review the plan against the approved spec and repository state.
5. Summarize the tasks, key boundaries, and verification strategy, then ask the
   user to approve the plan or request revisions.
6. After approval, change `Status` to `Approved` and ask the user to choose
   `formless:blatt-kuessen`, `formless:zeile-gehen`, or stop.

Do not start execution, commit, or invoke an execution skill without the user's
choice at the phase gate.

## Plan Format

Use every heading in this order. Write `None` when a section does not apply; do
not omit sections or invent a different structure.

```markdown
# [Feature Name] Implementation Plan

**Status:** Draft | Approved

**Source Spec:** `docs/formless/specs/YYYY-MM-DD-<topic>.md`

## Goal

[One observable sentence.]

## Background

[How the relevant system currently works, where the change belongs, and the
minimum context needed to understand the plan.]

## Architecture

[The chosen implementation approach and why it follows the approved spec.]

## Constraints

- [Binding project-wide requirement.]

## Context Map

- `path/to/source` - [What authoritative information to read here.]

## Tasks

### Task N: [coherent deliverable]

**Outcome:**

[Observable result produced by this task.]

**Context:**

[Why this task exists, what it depends on, and which files to read first.]

**Files:**

- Modify: `path/to/file`
- Create: `path/to/file`

**Decisions and Boundaries:**

- [chosen approach, binding constraint, or non-obvious behavior]

**Interfaces:**

- Consumes: [existing contract]
- Produces: [contract later tasks rely on]

**Verification:**

- [evidence that would detect failure; exact command when needed]

**Escalate if:**

- [condition the implementer must not guess about]
```

Do not use placeholders such as `TBD`, "handle edge cases", or "add appropriate
tests". If a fact is unknown, resolve it before handoff or make the discovery
step and decision boundary explicit.

## Self-Review

Before handoff, check:

1. Every requirement maps to a task.
2. Tasks are coherent deliverables rather than workflow fragments.
3. Cross-task names, types, and ordering agree.
4. Verification is proportionate and would detect a real failure.
5. No consequential choice has been silently delegated to the implementer.
6. No instruction dictates routine mechanics without reducing meaningful risk.
7. A capable implementer can distinguish freedom within the plan from a reason
   to escalate.
8. The background and context map identify authoritative files without copying
   their contents into every task.
9. Every fixed-format heading is present and the source spec is approved.
