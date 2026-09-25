# Learn New Technology

An agent skill for learning unfamiliar software technology through a fixed 20-layer observation map, one focused lesson at a time.

The skill combines comprehensive coverage with adaptive teaching:

- A fixed map prevents important dimensions from disappearing.
- A learning mission determines how deeply each dimension matters.
- Primary sources ground technical claims.
- Course files preserve lessons across chat sessions.
- Retrieval, predictions, and experiments provide evidence of learning.
- `--continue` chooses whether to review, deepen, experiment, or advance.

## Why this exists

Technology learning often starts with commands and tutorials. That can produce short-term familiarity without a reliable mental model. This skill studies a technology from its purpose and boundaries through architecture, state, data, failure, operations, internals, trade-offs, and independent application.

It never treats a delivered explanation as proof that the learner understood it.

## The 20-layer map

1. Identity and purpose
2. Context and boundaries
3. Inputs and outputs
4. Vocabulary and objects
5. Relationships and architecture
6. User interfaces
7. Processing flow
8. Lifecycle and state
9. Data and persistence
10. Configuration and environments
11. Failure and recovery
12. Observability and diagnosis
13. Resources and performance
14. Security and permissions
15. Installation, upgrades, and operations
16. Internal mechanisms
17. Limits and trade-offs
18. Ecosystem and alternatives
19. Experiments
20. Independent explanation and application

See [the full observation map](references/observation-map.md) for the questions and outputs associated with every layer.

## Installation

### Codex user skill

Clone the repository into the user skill directory:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/hieu3108/learning-new-technology.git \
  ~/.agents/skills/learn-new-technology
```

For a Codex setup that uses `CODEX_HOME/skills`, clone it there instead:

```bash
git clone https://github.com/hieu3108/learning-new-technology.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/learn-new-technology"
```

Restart Codex if the skill does not appear immediately.

### Repository-scoped skill

To make the skill available only inside one repository:

```bash
mkdir -p .agents/skills
git clone https://github.com/hieu3108/learning-new-technology.git \
  .agents/skills/learn-new-technology
```

## Usage

Start a course:

```text
$learn-new-technology Docker --start
```

The skill first establishes why you are learning, what you already know, the capability you need, and relevant constraints. It then teaches at most one layer per response.

Continue without deciding the pedagogical action yourself:

```text
$learn-new-technology Docker --continue
```

`--continue` reads the course state and chooses exactly one action:

1. clarify the mission;
2. evaluate a pending answer or experiment;
3. review an unverified layer;
4. deepen a misconception or run an experiment;
5. advance after sufficient evidence;
6. finish the course pass when the mission-relevant map is complete.

It performs one action and waits. It is not a background loop.

## Prompt conventions

The options are prompt conventions interpreted by the agent, not shell flags.

| Prompt | Result |
| --- | --- |
| `--start` | Start or load a course and establish its mission |
| `--continue` | Let the skill choose one evidence-based next action |
| `--mission` | Show or revise the learning mission |
| `--map` | Show the 20 layers and their statuses |
| `--course` | Show the course index and continuation point |
| `--next` | Explicitly move to the next layer, preserving learning debt |
| `--layer N` | Work on exactly one selected layer |
| `--deepen` | Stay on the current layer and go deeper |
| `--review` | Test retrieval or application without advancing |
| `--sources` | Inspect or improve the source ledger |
| `--save` | Persist state without starting another lesson |
| `--resume` | Load state and report the current continuation point |

Examples:

```text
$learn-new-technology PostgreSQL --map
$learn-new-technology Kafka --layer 9
$learn-new-technology React --review
$learn-new-technology Docker --course
```

## Persistent course workspace

Each technology gets an independent workspace:

```text
learning-notes/<technology>/
├── MISSION.md
├── RESOURCES.md
├── COURSE.md
├── PROGRESS.md
├── NOTES.md
├── lessons/
├── reference/
└── learning-records/
```

- `MISSION.md` records why the learner started and how the goal changes.
- `RESOURCES.md` records consulted sources and why they are trusted.
- `COURSE.md` is the human-facing table of contents.
- `PROGRESS.md` tracks all 20 layers, open questions, and learning debt.
- `lessons/` preserves the historical lesson context.
- `reference/` contains reusable glossaries, diagrams, and decision guides.
- `learning-records/` contains demonstrated knowledge rather than activity logs.

Because the workspace is stored on disk, a new chat session can continue the course:

```text
$learn-new-technology Docker --continue
```

Run that command from the workspace containing `learning-notes/docker/`, or provide the course path explicitly.

See [the workspace specification](references/workspace-format.md) for file formats and migration behavior.

## Evidence model

| Mark | Meaning |
| --- | --- |
| `○` | Not examined |
| `△` | Read or heard, not tested |
| `✓` | Retrieved, predicted, or observed once |
| `◆` | Explained causally and handled a variation |
| `?` | Open question |
| `A` | Untested assumption |
| `!` | Contradiction or unexpected result |
| `N/A` | Demonstrably inapplicable |

The skill may advance with unresolved optional depth when the mission does not require it. That gap remains visible as learning debt.

## Repository contents

```text
.
├── SKILL.md
├── README.md
├── LICENSE
└── references/
    ├── observation-map.md
    └── workspace-format.md
```

## Design influences

The stateful workspace, mission, trusted-resource ledger, lesson archive, and evidence-oriented learning records were inspired in part by Matt Pocock's [`teach`](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach) skill.

This project adds a fixed technology-specific 20-layer observation map, explicit progress states, mission-adjusted completion criteria, and guided `--continue` routing constrained by that map.

## Contributing

Issues and pull requests are welcome. Useful contributions include:

- clearer observation questions;
- realistic experiments for specific technology categories;
- improved progression and review behavior;
- corrections supported by primary sources;
- compatibility improvements for agent-skill hosts.

Please keep the core invariant: one response covers at most one learning layer.

## License

[MIT](LICENSE) © 2026 hieu3108
