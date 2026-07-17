---
name: worte-fangen
description: Use for brainstorming when a proposed feature or behavior change has unresolved requirements, meaningful design choices, or architectural trade-offs that need user input before implementation
---

# Worte fangen

Catch the words before they disappear. Turn an unformed idea into an approved
design by giving its important choices precise language.

This workflow is for decisions, not for adding ceremony before an already clear
change.

## Scope Gate

- If intent, behavior, constraints, and implementation direction are already
  clear, do not run this workflow. Proceed directly or use `satz-meisseln` when
  the work still needs a multi-task handoff.
- If consequential choices remain, explore them before implementation.
- If only one small point is unclear, ask that question directly rather than
  producing a full design process.

## Process

1. Inspect the relevant project context.
2. Ask one focused question at a time until purpose, constraints, and success
   criteria are clear.
3. Present viable approaches with trade-offs and a recommendation when there is
   a real choice. Do not manufacture alternatives for an obvious decision.
4. Present the design at a depth proportional to its complexity and obtain user
   approval for consequential decisions.
5. For a substantial design, write the approved spec to
   `docs/formless/specs/YYYY-MM-DD-<topic>-design.md`. For a small design,
   the approved conversation is sufficient unless the user requests a file.
6. Self-review for contradictions, placeholders, scope creep, and ambiguity.
7. Use `formless:satz-meisseln` only when implementation needs a multi-task
   handoff. Otherwise proceed with the direct change.

Do not commit the spec, start implementation, or invoke another workflow merely
to complete a checklist. User and repository instructions govern those actions.

## Design Content

Cover only what the task needs: architecture, boundaries, data flow, error
handling, compatibility, verification, and rollout considerations as relevant.
Follow existing project patterns and avoid unrelated refactoring.
