# Superpowers

Superpowers is a lightweight software development workflow for coding agents,
built from five composable skills.

## Quickstart

Give your agent Superpowers: [Claude Code](#claude-code), [Codex App](#codex-app), or [Codex CLI](#codex-cli).

## How it works

For obvious localized work, the agent makes the change directly and verifies it
with proportionate evidence. For complex work or a handoff to another model, it
writes a plan that preserves architectural decisions, interfaces, constraints,
and escalation points without fragmenting the work into ceremonial steps.

Once you say "go", *subagent-driven-development* assigns each coherent task to
a fresh implementer and reviews the result before continuing. The plan decides
the appropriate verification strategy. New tests are added when they protect
meaningful behavior and can catch a plausible regression, not merely because a
file changed.

Because the skills trigger automatically, you don't need to select one for every
request.

## Installation

Installation differs by harness. If you use more than one, install Superpowers separately for each one.

### Claude Code

Superpowers is available via the [official Claude plugin marketplace](https://claude.com/plugins/superpowers)

#### Official Marketplace

- Install the plugin from Anthropic's official marketplace:

  ```bash
  /plugin install superpowers@claude-plugins-official
  ```

#### Superpowers Marketplace

The Superpowers marketplace provides Superpowers and some other related plugins for Claude Code.

- Register the marketplace:

  ```bash
  /plugin marketplace add obra/superpowers-marketplace
  ```

- Install the plugin from this marketplace:

  ```bash
  /plugin install superpowers@superpowers-marketplace
  ```

### Codex App

Superpowers is available via the [official Codex plugin marketplace](https://github.com/openai/plugins).

- In the Codex app, click on Plugins in the sidebar.
- You should see `Superpowers` in the Coding section.
- Click the `+` next to Superpowers and follow the prompts.

### Codex CLI

Superpowers is available via the [official Codex plugin marketplace](https://github.com/openai/plugins).

- Open the plugin search interface:

  ```bash
  /plugins
  ```

- Search for Superpowers:

  ```bash
  superpowers
  ```

- Select `Install Plugin`.

## The Basic Workflow

1. **Direct execution** - Make clear, localized changes without creating a plan.

2. **brainstorming** - Resolve meaningful requirements or design choices when the direction is not yet clear.

3. **writing-plans** - For complex work or model handoff, define a small number of coherent deliverables with exact constraints, interfaces, and proportionate verification.

4. **subagent-driven-development** - Dispatch a fresh implementer per planned task and retain independent task and final review.

5. **executing-plans** - Execute a written plan inline when subagents are unavailable or not desired.

## What's Inside

### Skills Library

- **using-superpowers** - Lightweight workflow selection and platform bootstrap
- **brainstorming** - Resolve requirements and design trade-offs
- **writing-plans** - Create implementation handoffs with coherent task boundaries
- **subagent-driven-development** - Execute with fresh implementers, task review, and final review
- **executing-plans** - Execute plans inline without subagents

## Philosophy

- **Valuable verification** - Add tests when they protect meaningful behavior; otherwise use the evidence best suited to the actual risk
- **Systematic when needed** - Use process where it reduces meaningful risk
- **Complexity reduction** - Simplicity as primary goal
- **Evidence over claims** - Verify before declaring success

## Updating

Superpowers updates are somewhat coding-agent dependent, but are often automatic.

## License

MIT License - see LICENSE file for details
