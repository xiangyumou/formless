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
trade-offs with the user before implementation begins.

### 3. Sätze meißeln · Chisel the sentences

**Implementation planning and model handoff**

`saetze-meisseln` turns approved intent into a durable implementation plan. It
records boundaries, interfaces, constraints, verification, and escalation
points without fragmenting coherent work into ceremonial steps.

### 4. Das Blatt küssen · Kiss the page

**Subagent-driven development**

The first touch turns possibility into code. `das-blatt-kuessen` gives each
coherent plan task to a fresh implementer, checks the resulting evidence, and
uses independent task and final review before declaring the work complete.

### 5. Der Zeile folgen · Follow the line

**Direct plan execution**

`der-zeile-folgen` follows a written plan inline when subagents are unavailable
or unwanted. It executes continuously, preserves user changes, and verifies in
proportion to actual risk.

## How It Works

Formless does not require a workflow for every request. The entry skill chooses
among three paths:

1. Make an obvious localized change directly and verify it.
2. Catch unresolved decisions, then chisel a plan when coordination or handoff
   warrants one.
3. Execute an existing plan with fresh subagents or follow it directly.

Plans preserve decisions that should not be rediscovered. Tests are added when
they protect meaningful behavior and can catch a plausible regression;
otherwise the agent uses the most direct relevant evidence.

## Installation

Installation is harness-specific. Install Formless separately in each coding
agent where you want its skills to be available.

### Claude Code

Register this repository as a marketplace and install the plugin:

```bash
/plugin marketplace add xiangyumou/formless
/plugin install formless@formless-dev
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

- Approved designs: `docs/formless/specs/`
- Implementation plans: `docs/formless/plans/`
- Subagent execution state: `.formless/sdd/`

## Principles

- **Process only when it pays for itself** — direct work stays direct.
- **Decisions survive handoff** — plans preserve judgment, not busywork.
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
