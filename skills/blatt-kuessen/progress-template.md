# The Ledger

- Plan: `[PLAN_FILE]`
- Source spec: `[SPEC_FILE]`
- Execution mode: `subagent-driven`
- Branch: `[BRANCH]`
- Starting commit: `[START_SHA]`
- Current movement: `[TASK_AND_PHASE]`
- Updated: `[TIMESTAMP]`

## Task NN - [TITLE]

### Set the line

- Native task: `[TASK_ID]`
- State: `PENDING | BLOCKED | IN_PROGRESS | COMPLETE | NEEDS_ATTENTION`
- Agent: `task_NN_schreiber`
- Base: `[BASE_SHA]`
- Head: `[HEAD_SHA]`
- Report: `task-NN/implement.md`
- Verification: `[RESULT_OR_NONE]`
- Concern: `[CONCERN_OR_NONE]`

### Read the line

- Native task: `[TASK_ID]`
- Blocked by: `[SET_THE_LINE_TASK_ID]`
- State: `PENDING | BLOCKED | IN_PROGRESS | COMPLETE | NEEDS_ATTENTION`
- Lektor: `task_NN_lektor`
- Lektor agent ID: `[AGENT_ID_OR_PENDING]`
- Current review round: `[RR]`
- Verdict: `PENDING | APPROVED | NEEDS_FIXES`
- Minor findings: `[FINDINGS_OR_NONE]`

#### Round RR

- Lektor: `task_NN_lektor`
- Lektor agent ID: `[AGENT_ID]`
- Review mode: `INITIAL | RESUMED | REPLACEMENT`
- Review report: `task-NN/review-RR.md`
- Korrektor: `task_NN_korrektor_RR | None`
- Fix report: `task-NN/fix-RR.md | None`
- Round result: `APPROVED | NEEDS_FIXES | NEEDS_ATTENTION`

<!-- Keep one Lektor across rounds when the harness supports resumption. Append
one Round section per review/fix cycle; never replace earlier rounds. -->

## Final - Read the page

- Native task: `[TASK_ID]`
- Blocked by: `[LAST_READ_THE_LINE_TASK_ID]`
- State: `PENDING | BLOCKED | IN_PROGRESS | COMPLETE | NEEDS_ATTENTION`
- Current review round: `[RR]`
- Verdict: `PENDING | READY | NEEDS_FIXES`
- Remaining findings: `[FINDINGS_OR_NONE]`

#### Round RR

- Lektor: `werk_lektor_RR`
- Review report: `final/review-RR.md`
- Korrektor: `werk_korrektor_RR | None`
- Fix report: `final/fix-RR.md | None`
- Round result: `READY | NEEDS_FIXES | NEEDS_ATTENTION`

<!-- Append one Round section per final review/fix cycle; never replace earlier rounds. -->

## Next Mark

- Action: `[NEXT_ACTION]`
- Blocked by: `[BLOCKER_OR_NONE]`
