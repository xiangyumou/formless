---
name: zeile-gehen
description: Use for direct plan execution when following a written implementation plan without subagents or in a separate execution session
---

# Zeile gehen

Walk the line already set down. Execute a written implementation plan directly,
one coherent deliverable at a time.

Execute a written plan directly when subagent-driven development is unavailable
or the user chooses inline execution.

## Workspace Preparation

Read repository instructions and inspect the current branch, workspace, and
uncommitted changes. Reuse a suitable workspace. Do not implement on `main` or
`master` without explicit user permission; create a feature branch or worktree
only when isolation is actually needed. Preserve unrelated user changes.

## Execution

1. Read the plan once and check its constraints, task ordering, interfaces,
   verification requirements, and escalation conditions.
2. Raise genuine plan conflicts before implementation. Otherwise proceed
   continuously without asking for permission between tasks.
3. Execute each coherent task as one deliverable. Do not turn its internal
   implementation and verification actions into separate tasks.
4. Follow the plan's verification strategy. Add tests only when the plan's
   test-value criteria are met; do not invent coverage work during execution.
5. Inspect the diff after each task and record progress before continuing.

Stop for missing authority, an unresolved blocker, a contradiction, or an
unexpected decision the plan does not answer. Do not guess at architecture or
scope.

## Completion

Run the plan's final verification and report:

- tasks completed
- files and commits changed
- verification performed and results
- remaining concerns
- current branch and workspace state

Do not automatically run a broader suite than the plan requires. Do not merge,
push, create a PR, delete a branch, remove a worktree, or discard changes unless
the user explicitly requests it.

When subagents are available and the user wants independent review per task,
use `formless:blatt-kuessen` instead.
