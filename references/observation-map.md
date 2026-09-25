# A 20-layer observation map for learning technology

## Purpose

Use this map to study an unfamiliar programming technology from the outside in. It applies to tools such as Docker and Git, frameworks such as React, databases such as PostgreSQL, messaging systems such as Kafka, and platforms such as Kubernetes.

No finite checklist can cover every detail. These layers cover the dimensions that usually determine whether someone can understand, use, test, diagnose, and operate a technology. Add domain-specific branches inside the appropriate layer without changing the shared order.

## Route

```text
OUTSIDE VIEW
  01. Identity and purpose
  02. Context and boundaries
  03. Inputs and outputs

STATIC STRUCTURE
  04. Vocabulary and objects
  05. Relationships and architecture
  06. User interfaces

DYNAMIC BEHAVIOR
  07. Processing flow
  08. Lifecycle and state
  09. Data and persistence

REAL ENVIRONMENT
  10. Configuration and environments
  11. Failure and recovery
  12. Observability and diagnosis
  13. Resources and performance
  14. Security and permissions
  15. Installation, upgrades, and operations

INSIDE VIEW
  16. Internal mechanisms
  17. Limits and trade-offs
  18. Ecosystem and alternatives

VERIFIED UNDERSTANDING
  19. Experiments
  20. Independent explanation and application
```

---

## Layer 1 — Identity and purpose

Ask: “What is this, and why does it exist?”

- [ ] What is its precise name?
- [ ] Is it a library, framework, runtime, database, protocol, tool, or platform?
- [ ] Which concrete problem does it solve?
- [ ] Who normally uses it?
- [ ] What benefit reaches the final product or user?
- [ ] Can I describe it without jargon?

**Output:**

> `[Technology]` is a `[category]` that helps `[audience]` solve `[problem]` by `[main approach]`.

**Completion:** Explain its purpose to a developer who has never used it.

## Layer 2 — Context and boundaries

- [ ] Where does it sit in a larger system?
- [ ] What happens immediately before and after it?
- [ ] Which operating system, runtime, service, or technology does it depend on?
- [ ] Where does its responsibility begin and end?
- [ ] What does it explicitly not solve?
- [ ] When should it not be used?

**Output:**

```text
Upstream component → Technology → Downstream component
                           ↓
                    Dependencies
```

## Layer 3 — Inputs and outputs

- [ ] What inputs does it accept?
- [ ] Do inputs come from users, files, APIs, networks, or other programs?
- [ ] What outputs does it produce?
- [ ] Where are outputs returned, sent, or stored?
- [ ] What makes input valid or invalid?
- [ ] What side effects occur beyond the returned value?

**Output:** At least three `input → output` examples, including one failure.

## Layer 4 — Vocabulary and objects

For every core term, ask:

```text
What is it?
What is it for?
Who creates it?
Who uses it?
Where does it exist?
How long does it live?
How does it differ from the nearest concept?
```

- [ ] List the 10–20 core terms.
- [ ] Group them into objects, actions, states, and configuration.
- [ ] Identify easily confused pairs.
- [ ] Define them in your own words.
- [ ] Attach a concrete example to each important term.

**Output:** A working glossary rather than copied definitions.

## Layer 5 — Relationships and architecture

- [ ] What are the main components?
- [ ] Which component creates, calls, contains, or manages another?
- [ ] Are relationships one-to-one, one-to-many, or many-to-many?
- [ ] Which components share a process, and which do not?
- [ ] Which components share a machine, and which can be remote?
- [ ] Which are required and which are optional?

**Output:** A box-and-arrow diagram. Label every arrow with a verb such as `calls`, `reads`, `creates`, `stores`, or `sends`.

## Layer 6 — User interfaces

- [ ] Do users interact through a CLI, API, SDK, configuration file, or GUI?
- [ ] What is the smallest operation that produces a useful result?
- [ ] Which core operations create, read, update, and delete?
- [ ] What defaults are applied?
- [ ] Which parameters are commonly misunderstood?
- [ ] Where is the authoritative reference documentation?

**Output:** A minimal runnable example whose every line you can explain.

## Layer 7 — Processing flow

- [ ] What event starts the flow?
- [ ] Which component receives it first?
- [ ] In what order do processing steps occur?
- [ ] Which steps are synchronous or asynchronous?
- [ ] Where are network, disk, or process boundaries crossed?
- [ ] How does the result return to the caller?

**Output:** A sequence diagram or numbered successful path.

## Layer 8 — Lifecycle and state

- [ ] When is an object created?
- [ ] Which states can it enter?
- [ ] Which events cause transitions?
- [ ] When does it stop, expire, or get deleted?
- [ ] Can it restart or be reused?
- [ ] Which state survives a process or machine crash?

**Output:** A state diagram adapted to the actual technology.

## Layer 9 — Data and persistence

- [ ] What data is read or written?
- [ ] Does it live in memory, files, databases, or external systems?
- [ ] Which data is ephemeral and which is durable?
- [ ] Who owns the data?
- [ ] How long does it live?
- [ ] What data disappears when an object is deleted?
- [ ] Are caching, replication, backup, or migration involved?
- [ ] What consistency guarantees exist?

**Output:** `Data type → location → lifetime → recovery method`.

## Layer 10 — Configuration and environments

- [ ] Is it configured through files, environment variables, CLI flags, or APIs?
- [ ] What is the precedence between configuration sources?
- [ ] Which important defaults operate silently?
- [ ] How do development, test, and production differ?
- [ ] Does a configuration change require restart or reload?
- [ ] Are secrets separated from ordinary configuration?

**Output:** A minimal configuration and a production-oriented configuration, with differences explained.

## Layer 11 — Failure and recovery

- [ ] What happens with invalid input?
- [ ] What happens when a dependency is unavailable?
- [ ] What happens under network loss, full disk, low memory, or timeout?
- [ ] Is repeating an operation safe?
- [ ] Is partial work rolled back, retried, resumed, or abandoned?
- [ ] Which failures are transient or permanent?
- [ ] How do users and systems detect failure?

**Output:** `Failure → signal → consequence → recovery`.

## Layer 12 — Observability and diagnosis

- [ ] Where can current state be inspected?
- [ ] Where are logs and log levels?
- [ ] Are metrics, traces, events, or health checks available?
- [ ] How can you distinguish healthy from merely running?
- [ ] Which identifier follows work across components?
- [ ] What is the diagnostic sequence for “it does not work”?

**Output:** A diagnostic procedure that starts from symptoms rather than guesses.

## Layer 13 — Resources and performance

- [ ] How does it use CPU, memory, disk, and network?
- [ ] What are the common bottlenecks?
- [ ] Are there connection, request, process, or data limits?
- [ ] How are latency and throughput measured?
- [ ] Does it scale vertically, horizontally, or both?
- [ ] Which component fails first as load grows?
- [ ] Does it use caching, batching, pooling, or parallelism?

**Output:** A baseline measurement and one controlled load experiment.

## Layer 14 — Security and permissions

- [ ] Who can call or control it?
- [ ] How are identities authenticated?
- [ ] At what granularity are permissions granted?
- [ ] Is data encrypted in transit and at rest?
- [ ] Where are credentials and secrets stored?
- [ ] Where are the trust boundaries?
- [ ] What can untrusted input cause?
- [ ] Are default permissions broader than necessary?
- [ ] What is the blast radius of a compromised component?

**Output:** A trust-boundary diagram and the minimum required permissions.

## Layer 15 — Installation, upgrades, and operations

- [ ] What installation methods exist?
- [ ] Where do executables, configuration, data, and logs live?
- [ ] How do you identify the running version?
- [ ] How do you start, stop, and restart it?
- [ ] Does an upgrade require data migration?
- [ ] What compatibility guarantees exist?
- [ ] How do you roll back?
- [ ] What remains after uninstalling?
- [ ] How are backup and restore tested?

**Output:** A short install, upgrade, rollback, and uninstall runbook.

## Layer 16 — Internal mechanisms

Study this layer after behavior, lifecycle, and data are clear.

- [ ] Which code or process handles a core operation?
- [ ] Which operating-system or runtime primitives does it use?
- [ ] What core algorithms and data structures are involved?
- [ ] Which components schedule, store, communicate, or synchronize?
- [ ] How is concurrency controlled?
- [ ] How do caching and consistency interact?
- [ ] Can you trace one operation from user interface to the lowest relevant mechanism?

**Output:** A layered explanation of one core operation down to its underlying runtime or infrastructure.

## Layer 17 — Limits and trade-offs

- [ ] Which use cases is it optimized for?
- [ ] What does it trade away to gain those advantages?
- [ ] What technical limits are documented or observed?
- [ ] What looks easy in a demo but becomes difficult in production?
- [ ] Which assumptions must remain true?
- [ ] What failure patterns or misuses recur?
- [ ] What are the learning, operating, and migration costs?

Challenge every claim:

```text
Faster than what?
Simpler under which conditions?
Safe under which assumptions?
Where did the cost move?
```

## Layer 18 — Ecosystem and alternatives

- [ ] Which tools are commonly used with it?
- [ ] Which projects are official or third-party?
- [ ] What are the competing approaches?
- [ ] How do their models, scope, and trade-offs differ?
- [ ] Is there an open standard underneath?
- [ ] Does adoption create vendor lock-in?
- [ ] How healthy are its documentation, community, and release cadence?

**Output:** A comparison based on real needs, not feature counts.

## Layer 19 — Experiments

Use this loop for every important claim:

```text
1. Ask a question.
2. Write a prediction.
3. Change one factor.
4. Run the experiment.
5. Record the observation.
6. Compare it with the prediction.
7. Update the mental model.
8. Repeat with a boundary or failure case.
```

- [ ] Test a successful case.
- [ ] Test invalid input.
- [ ] Break a dependency.
- [ ] Restart and inspect surviving state.
- [ ] Change configuration.
- [ ] Apply a resource limit.
- [ ] Test one personal assumption.

**Experiment record:**

```text
Question:
Prediction:
Setup:
Changed factor:
Observed result:
Did it match?
Updated explanation:
Next question:
```

## Layer 20 — Independent explanation and application

Understanding is demonstrated when you can:

- [ ] Explain the technology without reading a definition.
- [ ] Draw its architecture from memory.
- [ ] Predict ordinary behavior.
- [ ] Explain why a result occurred.
- [ ] Diagnose a new failure from evidence rather than random commands.
- [ ] Build a small example without copying a tutorial.
- [ ] State when to use and avoid it.
- [ ] Compare it with at least one alternative.
- [ ] Apply it to a real problem.
- [ ] Clearly state what you still do not understand.

---

## Universal observation worksheet

```text
TECHNOLOGY:
START DATE:
LEARNING MISSION:

[01] IDENTITY AND PURPOSE
[02] CONTEXT AND BOUNDARIES
[03] INPUTS AND OUTPUTS
[04] VOCABULARY AND OBJECTS
[05] RELATIONSHIPS AND ARCHITECTURE
[06] USER INTERFACES
[07] PROCESSING FLOW
[08] LIFECYCLE AND STATE
[09] DATA AND PERSISTENCE
[10] CONFIGURATION AND ENVIRONMENTS
[11] FAILURE AND RECOVERY
[12] OBSERVABILITY AND DIAGNOSIS
[13] RESOURCES AND PERFORMANCE
[14] SECURITY AND PERMISSIONS
[15] INSTALLATION, UPGRADES, AND OPERATIONS
[16] INTERNAL MECHANISMS
[17] LIMITS AND TRADE-OFFS
[18] ECOSYSTEM AND ALTERNATIVES
[19] EXPERIMENTS
[20] INDEPENDENT EXPLANATION AND APPLICATION
```

## Progress marks

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

Aim for `◆` where the mission requires depth, `✓` for supporting knowledge, and explicit `△` or `?` elsewhere.

## Order rules

1. Use layers 1 through 20 as the shared coverage order.
2. Put newly encountered terminology in layer 4 rather than diving immediately into internals.
3. Attach every new question to a layer.
4. Enter layer 16 deeply only after flow, lifecycle, and data are understood.
5. Distinguish source claims, other people's reports, inference, and firsthand experiments.
6. Revisit the map whenever reality contradicts a prediction.
7. Completion means sufficient for the current mission, not exhaustive knowledge of the universe.
