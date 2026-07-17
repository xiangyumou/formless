---
name: saetze-meisseln
description: Use for implementation planning when a task is complex enough to require a multi-step handoff, or when the user explicitly asks for a written implementation plan
---

# Sätze meißeln

## Overview

Chisel fluid thought into durable sentences: write an implementation plan that
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
  model without the current context. Write a plan.
- **Unclear change:** important facts are missing. Investigate or ask before
  planning; do not turn uncertainty into invented steps.

## Planning For Handoff

Assume the implementer is capable but has no conversation history. Include:

- exact files, or precise discovery instructions when paths cannot yet be known
- intended behavior and acceptance criteria
- architectural decisions and constraints that must not be re-decided
- interfaces between tasks, including exact names and types when known
- verification commands or observable checks
- escalation conditions for ambiguity or unexpected repository state

Show exact code where the implementation is subtle or where a weaker model
could reasonably choose the wrong shape. Do not transcribe obvious changes
merely to make the plan look complete.

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

## Plan Format

Save plans to `docs/formless/plans/YYYY-MM-DD-<feature-name>.md` unless the
user requests another location.

```markdown
# [Feature Name] Implementation Plan

**Goal:** [one sentence]

**Architecture:** [the important approach and why]

**Global Constraints:**
- [exact project-wide requirement]

### Task N: [coherent deliverable]

**Files:**
- Modify: `path/to/file`
- Create: `path/to/file`

**Outcome:** [observable result]

**Implementation:**
- [specific decisions and changes]

**Interfaces:**
- Consumes: [existing contract]
- Produces: [contract later tasks rely on]

**Verification:**
- [exact command or visual/manual check]

**Escalate if:**
- [condition the implementer must not guess about]
```

Omit empty sections. Do not use placeholders such as `TBD`, "handle edge
cases", or "add appropriate tests". If a fact is unknown, resolve it before
handoff or make the discovery step and decision boundary explicit.

## Self-Review

Before handoff, check:

1. Every requirement maps to a task.
2. Tasks are coherent deliverables rather than workflow fragments.
3. Cross-task names, types, and ordering agree.
4. Verification is proportionate and would detect a real failure.
5. A weaker implementer can distinguish mechanical work from decisions that
   require escalation.

Then offer execution with `formless:das-blatt-kuessen` when
subagents are available. Do not require a separate execution workflow for a
direct change.
