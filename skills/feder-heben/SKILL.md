---
name: feder-heben
description: Use when starting a conversation where the Formless software-development workflow skills are available and the appropriate workflow must be selected
---

# Feder heben

Raise the quill. This is the entry point to Formless: choose the smallest
workflow that gives an unformed request enough structure to move forward.

Skills are tools, not mandatory ceremony. Use the smallest workflow that adds
material value, with user and repository instructions taking precedence.

## Asking Questions

When the runtime provides a native user-question tool, use it for consequential
question batches and phase-gate choices. Otherwise, ask in numbered text with
viable options, a recommendation, and a free-form alternative. Do not simulate
a native question UI in plain text when the tool is available.

## Workflow

Route work through the phases it actually needs:

1. Use `worte-fangen` to resolve consequential choices and produce an approved
   spec.
2. Use `satz-meisseln` to turn an approved spec into an approved implementation
   plan.
3. Use `blatt-kuessen` to execute the plan with fresh implementers and
   independent review, or `zeile-gehen` to execute it directly.
4. After execution, ask which delivery action comes next: review, commit, push,
   or pull request.

Make clear, localized changes directly when no design or implementation plan is
needed. After the direct change is verified, ask which delivery action the user
wants next.

## Phase Gates

Do not silently cross from spec to plan or from plan to execution. At the end of
each phase, summarize the completed artifact, state the available next actions,
and ask the user which action to take. Within an approved execution plan,
continue across clean tasks without pausing between them.

Do not load a process skill merely because the task is broadly related to its
topic. Announce a selected skill briefly, then follow it unless a more specific
instruction overrides it.

Read the matching platform file under `references/` only when tool adaptation
is needed.
