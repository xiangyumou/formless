---
name: blatt-kuessen
description: Use for subagent-driven development when executing an implementation plan with independent, reviewable tasks in the current session
---

# Blatt kuessen

Let the quill touch the blank page. Execute a written plan through fresh
subagents, turning each coherent task into reviewed code.

Execute a written plan with a fresh implementer for each coherent task, an
independent task review after each implementation, and one final review across
the complete change.

## Workspace Preparation

Before implementation:

1. Read repository instructions and inspect the current branch, worktree, and
   working-tree status.
2. Reuse an existing suitable workspace. Do not create a worktree merely
   because this skill was invoked.
3. Do not implement directly on `main` or `master` without explicit user
   permission. When isolation is needed, prefer the harness's native worktree
   capability; otherwise create a normal feature branch or project-local
   worktree according to repository conventions.
4. Preserve unrelated user changes. If they overlap the plan, work with them or
   ask when proceeding would be unsafe.
5. Record the starting commit for task and final review ranges.

## Start

Read the plan once. Extract its tasks, global constraints, interfaces,
verification requirements, and escalation conditions. Scan for contradictions
before Task 1 and present genuine conflicts as one batched question.

Use one implementer dispatch per plan task. Do not split a coherent plan task
into separate dispatches for testing, implementation, documentation, or
committing.

Track durable progress in `.formless/sdd/progress.md`. Resume from the first
task not recorded as complete; trust the ledger and git history after context
compaction.

## Per-Task Loop

For each task:

1. Record the current commit as `BASE`.
2. Run `scripts/task-brief PLAN_FILE N`; use the generated file as the task's
   single source of requirements.
3. Dispatch a fresh implementer using `implementer-prompt.md`. Provide only the
   brief path, necessary prior-task interfaces, workspace path, report path,
   and context the brief cannot contain.
4. Inspect the implementer's status and report. Never trust a completion claim
   without checking the diff and verification evidence.
5. Run `scripts/review-package BASE HEAD` and dispatch a fresh reviewer using
   `task-reviewer-prompt.md`.
6. Send Critical and Important findings to a fix subagent, repeat focused
   verification, and re-review until both spec compliance and task quality are
   approved.
7. Record the task's commit range and clean review in the progress ledger.

Do not pause between clean tasks. Stop only for an unresolved blocker, a real
plan conflict, missing authority, or completion of all tasks.

## Model Selection

Choose models by the judgment required:

- Mechanical work with complete instructions: fast model.
- Cross-file integration or incomplete prose instructions: standard model.
- Architecture, ambiguity resolution, and final review: most capable available
  model.
- Review: never use a model too weak to distinguish plan compliance from sound
  engineering judgment.

Always specify the subagent model explicitly when the harness supports it.

## Implementer Status

- `DONE`: package the diff and review it.
- `DONE_WITH_CONCERNS`: read the concerns, resolve correctness or scope doubts,
  then review.
- `NEEDS_CONTEXT`: provide only the missing context and resume the task.
- `BLOCKED`: diagnose whether the task needs context, a stronger model, a
  corrected plan, or human judgment. Do not retry unchanged.

## Review Boundaries

Task review is scoped to the task brief and its diff. The reviewer receives the
brief, implementer report, review package, and binding global constraints.

Do not ask reviewers to repeat verification without a concrete doubt. Do not
pre-judge findings or tell reviewers what not to flag. A finding that conflicts
with a plan-mandated choice goes to the user; neither the plan nor the reviewer
silently wins.

Minor findings go into the progress ledger for final-review triage. Critical and
Important findings block task completion.

## Final Review

After all task reviews pass:

1. Generate a review package from the recorded starting commit to `HEAD`.
2. Dispatch one capable reviewer using `final-reviewer-prompt.md`, including the
   plan path, review package, verification summaries, and recorded Minor items.
3. If findings require fixes, dispatch one fix subagent with the complete list,
   repeat the affected verification, regenerate the package, and re-review.

## Completion

Run the final verification required by the plan and any focused checks required
by review findings. Do not replace the plan's proportional verification with an
automatic full-suite run.

Report:

- tasks and commit ranges completed
- verification performed and results
- final-review verdict
- remaining concerns or Minor findings
- current branch and workspace state

Do not merge, push, create a PR, delete a branch, remove a worktree, or discard
changes unless the user explicitly requests that action.

## Internal Files

- `implementer-prompt.md`: task implementer contract
- `task-reviewer-prompt.md`: per-task spec and quality review
- `final-reviewer-prompt.md`: complete-change review
- `scripts/task-brief`: task extraction
- `scripts/review-package`: review artifact generation
- `scripts/sdd-workspace`: shared artifact workspace
