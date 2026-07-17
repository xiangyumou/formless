---
name: using-superpowers
description: Use when starting a conversation where Superpowers skills are available
---

# Using Superpowers

Superpowers skills are tools, not mandatory ceremony. Use the smallest workflow
that materially improves the current task.

## Selection Rule

Load a skill when the user names it or when its workflow clearly adds value.
User instructions and repository instructions take precedence. Do not invoke a
process skill merely because its description is broad or because the task is
technically related.

- Make obvious, localized, reversible changes directly with proportionate
  verification.
- Use `superpowers:writing-plans` for complex work, cross-component decisions,
  or a plan that another model will execute without this conversation.
- Use `superpowers:subagent-driven-development` to execute an existing plan with
  independent, reviewable tasks.
- Use other skills when explicitly requested or when their specialized process
  solves a concrete problem in the current task.

Announce a skill briefly when loading it. Once loaded, follow it unless it
conflicts with a more specific user or repository instruction.

For platform-specific subagent and tool mappings, read the matching file under
`references/` only when needed.
