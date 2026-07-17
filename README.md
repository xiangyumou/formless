# Superpowers

Superpowers is a complete software development methodology for your coding agents, built on top of a set of composable skills and some initial instructions that make sure your agent uses them.


## We're Hiring!

We're hiring someone to help out full time with Superpowers community and code work. 
You can read about the job at https://primeradiant.com/jobs/superpowers-community-engineer/
If this sounds like someone you know, definitely send them our way.

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

There's a bunch more to it, but that's the core of the system. And because the skills trigger automatically, you don't need to do anything special. Your coding agent just has Superpowers.

## Commercial Services

If you're using Superpowers in enterprise and could benefit from commercial support, additional tooling, or managed spending, please don't hesitate to drop us a line at sales@primeradiant.com.

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
- **Systematic over ad-hoc** - Process over guessing
- **Complexity reduction** - Simplicity as primary goal
- **Evidence over claims** - Verify before declaring success

Read [the original release announcement](https://blog.fsck.com/2025/10/09/superpowers/).

## Contributing

The general contribution process for Superpowers is below. Keep in mind that we don't generally accept contributions of new skills and that any updates to skills must work in Claude Code and Codex.

1. Fork the repository
2. Switch to the 'dev' branch
3. Create a branch for your work
4. Review the complete diff and verify changed plugin behavior
5. Submit a PR, being sure to fill in the pull request template.

Behavior evaluation, when needed, is maintained separately in [superpowers-evals](https://github.com/prime-radiant-inc/superpowers-evals/).

## Updating

Superpowers updates are somewhat coding-agent dependent, but are often automatic.

## License

MIT License - see LICENSE file for details

## Visual companion telemetry

Because skills and plugins don't provide any feedback to creators, we have no idea how many of you are using Superpowers. By default, the Prime Radiant logo on brainstorming's optional visual companion feature is loaded from our website. It includes the version of Superpowers in use. It does not include any details about your project, prompt, or coding agent. We don't see your clicks or anything about what you're building. This helps us have a rough idea of how many folks are using Superpowers and which version of Superpowers they're using. It's 100% optional. To disable this, set the environment variable `SUPERPOWERS_DISABLE_TELEMETRY` to any true value. Superpowers also honors Claude Code's `DISABLE_TELEMETRY` and `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` opt-outs.

## Community

Superpowers is built by [Jesse Vincent](https://blog.fsck.com) and the rest of the folks at [Prime Radiant](https://primeradiant.com).

- **Discord**: [Join us](https://discord.gg/35wsABTejz) for community support, questions, and sharing what you're building with Superpowers
- **Issues**: https://github.com/obra/superpowers/issues
- **Release announcements**: [Sign up](https://primeradiant.com/superpowers/) to get notified about new versions
