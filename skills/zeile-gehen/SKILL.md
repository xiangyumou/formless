---
name: zeile-gehen
description: Use for direct plan execution when following a written implementation plan without subagents or in a separate execution session
---

# Zeile gehen

## Invocation

Begin the first user-facing progress update with exactly:

> Walk the line to its end.

Say it once. Do not repeat it after context compaction or between tasks.

Follow what has already been set down. Execute a written implementation plan
directly, one coherent deliverable at a time.

Execute a written plan directly when subagent-driven development is unavailable
or the user chooses inline execution.

## Workspace Preparation

Read repository instructions and inspect the current branch, workspace, and
uncommitted changes. Reuse a suitable workspace when it is already on a
non-primary branch. When the current branch is `main` or `master`, create and
switch to a feature branch before implementation without asking for separate
permission. Execute directly on `main` or `master` only when the user explicitly
requests it. Preserve unrelated user changes.

## Execution

1. Verify that the plan and its source spec exist and their decisions are
   resolved. Treat the request to execute the plan as approval; do not ask the
   user to approve it again. Return to the appropriate phase only if an artifact
   is missing or a decision is unresolved.
2. Read the plan once, read the files in its context map, and check its
   constraints, task ordering, interfaces, verification requirements, and
   escalation conditions.
3. Raise genuine plan conflicts as one batched question with viable answers and
   a recommendation, using the runtime's native user-question tool when it is
   available. Otherwise proceed
   continuously without asking for permission between tasks.
4. Execute each coherent task as one deliverable. Do not turn its internal
   implementation and verification actions into separate tasks.
5. Follow the plan's verification strategy. Add tests only when the plan's
   test-value criteria are met; when no test is added, perform and record the
   plan's targeted alternative verification. Do not invent coverage work during
   execution.
6. Inspect the diff after each task and record progress before continuing.

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

After reporting completion, ask the user which delivery action comes next:
additional review, commit, push, pull request, or stop. Provide a recommendation
based on the current repository state. Do not perform the selected action until
the user chooses it.

Do not automatically run a broader suite than the plan requires. Do not merge,
push, create a PR, delete a branch, remove a worktree, or discard changes unless
the user explicitly requests it.

When subagents are available and the user wants independent review per task,
use `formless:blatt-kuessen` instead.
