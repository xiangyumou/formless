# Formless

*Raise the quill. Give form to what is not yet formed.*

Formless is a compact software-development workflow for coding agents. Five
composable skills carry work from an unresolved idea to reviewed
implementation without imposing process where a direct change is enough.

## The Five Movements

### 1. Feder heben · Raise the quill

**Entry and workflow selection**

The quill pauses above the page. `feder-heben` reads the shape of the request
and selects the smallest workflow that adds material value. Clear, localized
work proceeds directly.

### 2. Worte fangen · Catch the words

**Brainstorming and design**

An idea is still a ghost until its consequential choices have names.
`worte-fangen` resolves requirements, design decisions, and architectural
trade-offs in a single question batch with viable answers and a recommendation,
then records the resolved result in a fixed-format specification.

### 3. Satz meisseln · Chisel the sentence

**Implementation planning and model handoff**

`satz-meisseln` turns a resolved specification into a fixed-format
implementation plan. It records background, authoritative context files,
boundaries, interfaces, verification, and escalation points without
fragmenting coherent work into ceremonial steps.

### 4. Blatt kuessen · Kiss the page

**Subagent-driven development**

The first touch turns possibility into code. `blatt-kuessen` gives each
coherent plan task to a fresh implementer, checks the resulting evidence, and
uses independent task and final review before declaring the work complete.

### 5. Zeile gehen · Walk the line

**Direct plan execution**

`zeile-gehen` walks the line of a written plan when subagents are unavailable
or unwanted. It executes continuously, preserves user changes, and verifies in
proportion to actual risk.

## How It Works

Formless does not require every phase for every request. The full workflow is:

1. **Brainstorm:** inspect the project and ask all known consequential questions
   together, with options and recommended answers.
2. **Spec:** save the resolved design in the required format and ask the user
   whether to proceed to planning.
3. **Plan:** turn the resolved spec into a required-format implementation plan
   with global background and task-level context pointers, then ask the user to
   choose execution, revisions, or stop.
4. **Execute:** when the user asks to execute a plan, treat the request as plan
   approval and run it continuously with fresh subagents or directly. Do not
   ask for a separate approval.
5. **Deliver:** report the completed work and ask whether to review, commit,
   push, open a pull request, or stop.

Each phase ends at an explicit user gate, but a request to execute an existing
plan is itself the execution choice and approval. Clean tasks do not pause
between steps. Plan execution defaults to a feature branch; it runs directly on
`main` or `master` only when the user explicitly requests that. An obvious
localized change may skip spec and plan, proceed directly, and end at the
delivery gate.

Plans preserve decisions that should not be rediscovered. Every behavior change
has targeted verification. Tests are added when they protect meaningful behavior
and can catch a plausible regression; otherwise the plan records why and uses
alternative evidence that can detect the primary failure mode.

## Installation

Installation is harness-specific. Install Formless separately in each coding
agent where you want its skills to be available.

### Claude Code

Register this repository as a marketplace and install the plugin:

```bash
/plugin marketplace add xiangyumou/formless
/plugin install formless@formless
```

### Codex

Formless includes a Codex plugin manifest and marketplace metadata. Add the
repository through the Codex plugin interface, then select **Formless** from the
Developer Tools category.

Subagent-driven execution requires Codex multi-agent support:

```toml
[features]
multi_agent = true
```

## Runtime Artifacts

- Specifications: `docs/formless/specs/YYYY-MM-DD-<topic>.md`
- Implementation plans: `docs/formless/plans/YYYY-MM-DD-<topic>.md`
- Subagent execution state: `.formless/sdd/`

Specs and plans use fixed heading order and required fields. Plans link to their
resolved source spec. Global background explains the system and
points to authoritative files; task context explains only what that task needs
and where to read further.

## Principles

- **Process only when it pays for itself** — direct work stays direct.
- **Decisions survive handoff** — plans preserve judgment, not busywork.
- **Questions arrive together** — consequential choices include viable answers
  and a recommendation.
- **Phases require consent** — spec, plan, and delivery have explicit user
  gates; asking to execute a plan supplies execution consent and approval.
- **Evidence over claims** — completion requires relevant verification.
- **Coherent units of work** — implementation, verification, and review stay
  aligned around useful deliverables.
- **Complexity reduction** — the workflow should leave the system simpler than
  it found it.

## Lineage

Formless is a poetic reimagining of the Superpowers agent workflow created by
Jesse Vincent and contributors. The original copyright and MIT license are
preserved in [LICENSE](LICENSE).

## License

MIT
