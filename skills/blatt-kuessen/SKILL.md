---
name: blatt-kuessen
description: Use for subagent-driven development when executing an implementation plan with independent, reviewable tasks in the current session
---

# Blatt kuessen

## Invocation

Begin the first user-facing progress update with exactly:

> Let the quill kiss the page.

Say it once. Do not repeat it after context compaction or between tasks.

The first mark turns intention into code. Execute a written plan through named
subagents, one reviewed line at a time.

Execute a written plan with a fresh implementer for each coherent task, an
independent task Lektor whose context is preserved through that task's
fix/re-review loop, and one fresh final review across the complete change.

## Prepare the Page

Before implementation:

1. Read repository instructions and inspect the current branch, worktree, and
   working-tree status.
2. Reuse an existing suitable workspace when it is already on a non-primary
   branch. Do not create a worktree merely because this skill was invoked.
3. When the current branch is `main` or `master`, create and switch to a feature
   branch before implementation without asking for separate permission. Execute
   directly on `main` or `master` only when the user explicitly requests it.
   When stronger isolation is needed, prefer the harness's native worktree
   capability or a project-local worktree according to repository conventions.
4. Preserve unrelated user changes. If they overlap the plan, work with them or
   ask when proceeding would be unsafe.
5. Record the starting commit for task and final review ranges.

## Read What Is Written

Verify that the plan and its source spec exist and their decisions are resolved.
Treat the request to execute the plan with subagents as approval; do not ask the
user to approve it again. If an artifact is missing or a decision is unresolved,
stop and return to the appropriate phase instead of reconstructing decisions
during execution.

Read the plan once. Read the files in its context map, then extract its tasks,
global constraints, interfaces, verification requirements, and escalation
conditions. Scan for contradictions before Task 1 and present genuine conflicts
as one batched question with viable answers and a recommendation, using the
runtime's native user-question tool when it is available.

Use one implementation dispatch per plan task. Testing, documentation,
verification, and committing remain inside that coherent implementation; the
execution task list exposes responsibility and gates, not keystrokes.

## The Ledger

The controller owns task state. Subagents report their own work but never create,
complete, reorder, or otherwise maintain the global task list or
`.formless/sdd/progress.md`.

Before the first dispatch, resolve the artifact root with
`scripts/sdd-workspace` and initialize its `progress.md` from
`progress-template.md`. All `task-NN/` and `final/` paths below are relative to
that root. When the runtime provides native task management, also create this
live task view for every plan task:

- `[TNN - Set the line] <plan task title>` - implementation
- `[TNN - Read the line] <plan task title>` - review and its fix/re-review loop

Make each `Read the line` task depend on its matching `Set the line` task. Make
the next plan task's `Set the line` depend on the preceding `Read the line` task.
Create `[Final - Read the page] Complete change`, blocked by the final plan
task's `Read the line`. Use the native dependency mechanism when available;
otherwise enforce the same order from the ledger.

In Claude Code, encode these edges with the native `blockedBy` relationship (or
its equivalent task-update field), not as prose in the task description. A
blocked task remains pending until every recorded predecessor is complete.

The native task list is the live view; the ledger is the durable workflow state;
Git commits and immutable reports are the evidence. Before every dispatch,
after every subagent return, and after context compaction, reconcile all three.
Update the native task and ledger immediately at each transition. Never postpone
task maintenance until the end of a long implementation.

Every dispatch writes a new report. Never overwrite or append another agent's
report; add each review and fix round to the ledger as a new history entry.

Use native states such as `pending`, `in_progress`, and `completed` as provided
by the runtime. In the ledger, record `PENDING`, `BLOCKED`, `IN_PROGRESS`,
`COMPLETE`, or `NEEDS_ATTENTION`. A task with an unfinished predecessor remains
pending and blocked. If records disagree, inspect Git and the named reports,
repair the task view and ledger, and ask only when the evidence is genuinely
ambiguous.

## Set and Read Each Line

For each plan task:

1. Confirm its `Set the line` task is unblocked, mark it `in_progress`, record
   the transition in the ledger, and record the current commit as `BASE`.
2. Run `scripts/task-brief PLAN_FILE N`. Use the generated brief as the task's
   single source of requirements.
3. Dispatch `task_NN_schreiber` with `implementer-prompt.md`, the brief path,
   necessary prior-task interfaces, workspace path, and
   `task-NN/implement.md` report path.
4. Inspect the Schreiber's status, commits, report, diff, and verification
   evidence. When the implementation evidence is sound, mark `Set the line`
   complete and immediately move the matching `Read the line` task to
   `in_progress`.
5. Generate `task-NN/review-RR.diff` for the fixed `BASE..HEAD` range. Dispatch
   `task_NN_lektor` with `task-reviewer-prompt.md` and
   `task-NN/review-RR.md` as its report path. Give the Lektor the implementation
   report and every prior fix report for this task. Capture the actual agent ID
   returned by the harness immediately and write it to the ledger; the fixed
   name expresses the role, but the ID is the durable resumption handle.
6. If Critical or Important findings remain, dispatch
   `task_NN_korrektor_RR` with `fixer-prompt.md` and
   `task-NN/fix-RR.md`. Check its commit and focused verification, regenerate a
   fixed-SHA review package, and increment the review round. When the harness
   supports resumption, send the re-review follow-up from
   `task-reviewer-prompt.md` to the recorded Lektor agent ID. Resume that same
   Lektor for every round of this task so it retains the original brief,
   findings, tool evidence, and reasoning.
7. When both review verdicts are approved, record Minor findings for final
   triage, mark `Read the line` complete in both task systems, and allow the next
   blocked task to begin.

Never rely on a display name to resume a completed subagent when an agent ID is
available. If the ID is missing, the harness cannot resume it, or resumption
fails, dispatch a replacement Lektor with the full task brief, implementation
report, complete review/fix report chain, and current review package. Record the
replacement's ID and the fallback in the ledger, then resume that replacement
for later rounds when possible.

Do not pause between clean tasks. Stop only for an unresolved blocker, a real
plan conflict, missing authority, or completion of all tasks.

## Read the Evidence

Treat a successful deterministic command as an established execution fact when
the responsible Schreiber or Korrektor records its exact command, commit, scope,
exit status, result, and duration. The recorded commit must be the reviewed head,
or an ancestor whose later changes do not invalidate the result. Do not rerun
that same command merely to confirm that it succeeded. Instead, inspect the diff
and record to determine whether the command's scope and assertions actually
cover the changed behavior.

Repeat or request verification only when the record is incomplete, the code
changed after it ran, the command failed or was skipped, the result is
nondeterministic or environment-dependent, or code review identifies a concrete
unanswered risk. This does not limit normal code review or lightweight focused
checks.

## Name the Hands

Use these exact subagent names when the harness supports names. When it supports
only descriptions, begin the description with the same name:

- `task_NN_schreiber` - the one implementation dispatch for plan Task NN
- `task_NN_lektor` - task reviewer retained across every review round for Task NN
- `task_NN_korrektor_RR` - fixer for findings from review round RR
- `werk_lektor_RR` - complete-change reviewer for final round RR
- `werk_korrektor_RR` - fixer for findings from final round RR

Use two-digit task and round numbers. Names identify responsibility; immutable
report paths identify rounds; harness agent IDs identify resumable transcripts.
Do not invent aliases or reuse a completed subagent for a different role.

## Choose the Models

Choose models by role, not by perceived task difficulty:

- Implementation roles include every task implementer, every subagent fixing
  task-review findings, and every subagent fixing final-review findings. In
  Claude Code, use Sonnet for all implementation roles.
- Review roles include every task reviewer and the final reviewer. In Claude
  Code, use Opus for all review roles.
- In other agent harnesses, use the model with the equivalent positioning:
  the Sonnet-equivalent implementation model for implementation and fixes, and
  the Opus-equivalent highest-capability reasoning model for every review.

Never assign a review model based on implementation cost or simplicity, and
never turn a fix into a review role because it is difficult. Always specify the
subagent model explicitly when the harness supports it.

## Model Gate

Before every dispatch, name the role and set its model explicitly. In Claude
Code, this gate is mandatory:

- `Schreiber` and every `Korrektor`: `model: Sonnet`
- `Lektor` and every `Werk Lektor`: `model: Opus`

This includes replacement agents and every new final-review round. A dispatch
with an omitted model is invalid: do not let it inherit the controller's model;
correct the dispatch before sending it. Do not use Opus to implement or fix, and
do not use Sonnet to review, even when the task looks small or difficult.

## Read the Schreiber's Return

- `DONE`: package the diff and review it.
- `DONE_WITH_CONCERNS`: read the concerns, resolve correctness or scope doubts,
  then review.
- `NEEDS_CONTEXT`: provide only the missing context and resume the task.
- `BLOCKED`: diagnose whether the task needs context, a stronger model, a
  corrected plan, or human judgment. Do not retry unchanged.

## Read the Margin

Task review is scoped to the task brief and its diff. The Lektor receives the
brief, implementation report, every prior fix report, review package, and
binding global constraints.

Do not ask reviewers to repeat verification without a concrete doubt. Do not
pre-judge findings or tell reviewers what not to flag. A finding that conflicts
with a plan-mandated choice goes to the user; neither the plan nor the reviewer
silently wins.

Minor findings go into the progress ledger for final-review triage. Critical and
Important findings block task completion.

## Speak When the Line Breaks

Subagents normally work independently and return one complete report when their
dispatch ends. Do not turn routine progress into a stream of messages. When the
harness supports agent-to-controller messaging, contact the controller during a
dispatch only for a blocker, an invalidated plan, a consequential requirement or
design conflict, or a discovery that changes another task. In Claude Code, send
that exceptional message to `main`; ordinary completion still uses the normal
return and immutable report.

## Read the Whole Page

After all task reviews pass:

1. Move `[Final - Read the page] Complete change` to `in_progress` in the native
   task view and ledger. Generate `final/review-RR.diff` for the fixed starting
   commit through the current `HEAD`.
2. Dispatch `werk_lektor_RR` with `final-reviewer-prompt.md`, the plan path,
   review package, verification summaries, recorded Minor items, and
   `final/review-RR.md` as its report path.
3. If findings require fixes, dispatch `werk_korrektor_RR` with
   `fixer-prompt.md`, the complete finding list, and `final/fix-RR.md`. Check its
   commit and focused verification, regenerate the fixed-SHA package, increment
   the round, and send a fresh `werk_lektor_RR`.
4. Mark the final task complete only when the complete-change verdict is Ready
   and its report is recorded in the ledger.

## Close the Work

Run the final verification required by the plan and any focused checks required
by review findings. Do not replace the plan's proportional verification with an
automatic full-suite run.

Report:

- tasks and commit ranges completed
- verification performed and results
- final-review verdict
- remaining concerns or Minor findings
- current branch and workspace state

After reporting completion, ask the user which delivery action comes next:
additional review, commit, push, pull request, or stop. Provide a recommendation
based on the current repository state. Do not perform the selected action until
the user chooses it.

Do not merge, push, create a PR, delete a branch, remove a worktree, or discard
changes unless the user explicitly requests that action.

## Internal Files

- `implementer-prompt.md`: task implementer contract
- `task-reviewer-prompt.md`: per-task spec and quality review
- `fixer-prompt.md`: task and final finding-resolution contract
- `final-reviewer-prompt.md`: complete-change review
- `progress-template.md`: durable controller-owned ledger template
- `scripts/task-brief`: task extraction
- `scripts/review-package`: review artifact generation
- `scripts/sdd-workspace`: shared artifact workspace
