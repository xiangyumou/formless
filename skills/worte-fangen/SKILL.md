---
name: worte-fangen
description: Use for brainstorming when a proposed feature or behavior change has unresolved requirements, meaningful design choices, or architectural trade-offs that must be resolved with the user and recorded in a fixed-format specification before implementation planning
---

# Worte fangen

## Invocation

Begin the first user-facing progress update with exactly:

> Catch the words before they scatter.

Say it once. Do not repeat it after context compaction or within later question
batches.

Gather what is still unformed. Resolve consequential choices and turn the idea
into a specification whose decisions can guide the next phase.

This workflow is for decisions, not ceremony. If intent, behavior, constraints,
and implementation direction are already clear and the change is localized,
proceed directly. If implementation needs coordination or handoff, produce a
spec before writing a plan.

## Question Batch

Inspect the relevant project context before asking questions. Ask all currently
known consequential questions in one numbered batch instead of revealing them
one at a time.

Use the runtime's native user-question tool when it is available. Otherwise,
ask the batch in numbered text. The same rule applies to follow-up questions
and the next-phase choice at each phase gate.

For each question:

- state the decision in concrete terms
- provide two to four viable answers when real alternatives exist
- mark one answer as **Recommended** and explain why briefly
- allow a free-form answer when the listed choices do not fit

Tell the user they may reply with "use all recommended answers." Do not ask for
facts available in the repository, manufacture alternatives for an obvious
choice, or mix unrelated low-value questions into the batch. Ask a second batch
only when the first answers reveal new consequential uncertainty.

## Process

1. Inspect the repository, existing behavior, constraints, and relevant source
   files.
2. Ask one complete question batch covering purpose, scope, behavior, important
   trade-offs, compatibility, and success criteria as applicable.
3. Resolve follow-up uncertainty in one additional batch when necessary.
4. Write the spec to
   `docs/formless/specs/YYYY-MM-DD-<topic>.md` using the exact format below.
5. Self-review the spec for contradictions, unresolved placeholders, scope
   creep, missing decisions, and unverifiable acceptance criteria.
6. Summarize the spec and ask the user whether to proceed to
   `formless:satz-meisseln`, request revisions, or stop.
7. Before moving on, ensure `Open Questions` says `None` and that the user has
   explicitly selected the planning phase.

Do not write an implementation plan, start implementation, commit, or invoke
the next phase without the user's choice at the phase gate.

## Spec Format

Use every heading in this order. Write `None` when a section does not apply; do
not omit sections or invent a different structure.

```markdown
# [Feature Name] Specification

## Problem

[What is wrong, missing, or newly required.]

## Goals

- [Observable outcome.]

## Non-Goals

- [Explicitly excluded scope.]

## Background

[How the relevant system currently works and why this change belongs here.]

## Decisions

### [Decision Name]

**Choice:** [Selected direction]

**Rationale:** [Why this direction was selected]

## Design

[Architecture, boundaries, and behavior at the depth required by the change.]

## Interfaces and Data Flow

[Important inputs, outputs, contracts, state transitions, or `None`.]

## Errors and Edge Cases

- [Failure or boundary behavior.]

## Compatibility and Rollout

[Migration, compatibility, rollout implications, or `None`.]

## Acceptance Criteria

- [Observable criterion that proves the design is satisfied.]

## Open Questions

- [Unresolved question, or `None` when the decisions are resolved.]
```
