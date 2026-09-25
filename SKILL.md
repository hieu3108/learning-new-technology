---
name: learn-new-technology
description: Teach a programming technology through one selected layer at a time using a reusable 20-layer observation map, a concrete learning mission, trusted sources, and evidence-based progress. Use for systematic study of a tool, framework, database, protocol, platform, or unfamiliar codebase. Do not activate for a narrow implementation or debugging task unless the user asks to learn the underlying technology.
---

# Learn a technology by observation and evidence

Guide a long-running study without overwhelming the learner. Preserve the fixed 20-layer order in [the observation map](references/observation-map.md). Use [the workspace format](references/workspace-format.md) for persistent state.

## Invariants

- Cover at most one layer in a response. `--map`, onboarding, source maintenance, and progress review are not lessons and must not include a layer lesson.
- Keep the 20 layers as the coverage map. Adapt depth and examples to the learner's mission; do not let adaptation silently remove a layer.
- Treat model memory as unverified. Ground technical claims in current primary sources, record those sources, and cite them near the lesson claim. A citation makes verification easier; it does not make the claim infallible.
- Separate four kinds of knowledge: source claim, observed result, inference, and untested assumption.
- A delivered explanation is not evidence of learning. Promote progress only after retrieval, prediction, explanation, or a relevant experiment.
- Keep the course workspace and its reviewable lessons in the current workspace, never in the installed skill directory.

## Prompt conventions

These are natural-language conventions, not executable CLI flags. Accept equivalent wording.

| Convention | Behavior |
| --- | --- |
| `$learn-new-technology Docker` or `--start` | Load an existing study; otherwise establish its mission before teaching. |
| `--mission` | Show or revise the learning purpose, prior knowledge, target capability, and constraints. Do not teach a layer. |
| `--firstclass` | Alias for `--layer 1`. |
| `--map` | Show only the 20 layer names and statuses. Do not teach them. |
| `--continue` | Read the course state and choose exactly one next action: clarify mission, review, deepen/experiment, or teach the next layer. |
| `--next` | Move to the next layer. Preserve unresolved learning debt rather than marking it complete. |
| `--layer N` | Teach exactly layer N, from 1 through 20. Preserve earlier gaps. |
| `--deepen` | Stay on the current layer and use a concrete example, counterexample, or experiment. |
| `--review` | Retrieve or test the current layer. Evaluate the answer on the following turn; do not advance. |
| `--sources` | Show, verify, or improve the source ledger. Do not teach a layer unless explicitly combined with one. |
| `--course` | Show the course index: mission, completed lessons, references, records, and next lesson. Do not teach a layer. |
| `--save` | Persist the current state and current lesson without adding another lesson. |
| `--resume` | Load state and report the current layer, due review, open question, and next action. Do not advance. |

When options combine, obey the most specific layer and action. `--layer 8 --review` reviews layer 8. `--resume --next` loads state then advances one layer. `--continue` is incompatible with `--next`, `--review`, and `--deepen` because its purpose is to choose among them; if combined, honor the explicit action and ignore `--continue`. If options conflict, explain the conflict briefly and take the least expansive action. With no option, never advance more than one layer.

## Establish the mission

Before the first lesson, obtain or infer:

1. the real task or reason for learning;
2. relevant prior knowledge and terms the learner can already explain;
3. target capability: orientation, use, debugging, operation, internal mechanism, or teaching others;
4. practical constraints such as environment, time, or a current project.

Ask only for missing information that changes the course. Bundle the questions in one short onboarding response. Include one simple baseline prompt that asks the learner to explain what they currently believe; do not turn onboarding into an exam. Record uncertainty instead of inventing a learner profile.

Create `learning-notes/<technology-slug>/` only after the technology and mission are sufficiently clear. Initialize `MISSION.md`, `RESOURCES.md`, `COURSE.md`, `PROGRESS.md`, `NOTES.md`, `lessons/`, `reference/`, and `learning-records/` as defined by the workspace format. If a legacy `learning-notes/<technology-slug>.md` exists, preserve it and migrate its facts into the structured files on the next save or resume.

## Ground the lesson

Before teaching a layer, identify a primary source appropriate to that layer: official documentation or specification, source code, an original paper, or a maintainer publication. Prefer an observable experiment when the claim can be tested locally. Add useful sources to `RESOURCES.md`, including the layer, trust reason, verification date, and status.

Do not turn source collection into indiscriminate research. One strong primary source is enough for an ordinary lesson. Add another only when the first leaves a consequential gap or the topic depends on competing implementations. Label operational judgement and community practice as such; primary documentation may not establish them.

## Teach one layer

Read only the selected layer's section from the observation map. Produce a lesson small enough for one sitting:

1. `Layer N/20 — [name]` and why this lens matters to the mission.
2. One concrete example tied to the technology.
3. Two or three observation questions.
4. One prediction, explanation prompt, or small experiment.
5. A completion criterion phrased as `Complete this layer when you can...`.
6. Known facts, assumptions, and one open question.
7. One primary source worth opening.

Do not recite the full checklist unless the user requests the full checklist for this one layer. Define unfamiliar terms before relying on them. If the lesson is too easy or too hard, adjust the next response and record the preference in `MISSION.md`.

After presenting a new lesson or materially deepening one, save a self-contained Markdown lesson under `lessons/`. Include its date, the mission at that time, layer, explanation, example, observation questions, exercise, completion criterion, source links, assumptions, and next action. Preserve the first version's historical context; if later corrections are necessary, add a clearly dated correction or superseding lesson instead of silently rewriting what the learner originally received. Update `COURSE.md` with a link and one-line outcome.

Put durable material that the learner will repeatedly consult—glossaries, command tables, decision guides, or diagrams—in `reference/`. Do not duplicate whole lessons there. Create a reference only when reusable material actually exists.

## Review and advancement

Use retrieval before rereading. Ask the learner to explain, predict, compare, diagnose, or perform a small task without copying the lesson. Give feedback on the learner's reasoning, then correct gaps with the smallest useful explanation.

Use these statuses:

| Mark | Evidence |
| --- | --- |
| `○` | Not examined |
| `△` | Read or heard; no retrieval or test yet |
| `✓` | Correctly retrieved, predicted, or observed once |
| `◆` | Explained causally and handled a meaningful variation |
| `?` | Open question |
| `A` | Untested assumption |
| `!` | Contradiction or unexpected result |
| `N/A` | Shown to be inapplicable, with a reason |

The completion criterion is a gate for `✓` or `◆`, not a ban on exploration. If the learner requests `--next` before meeting it, proceed but keep the earlier layer `△` and record the review debt. On `--resume`, recommend a due review before new material when it would materially improve retention, while respecting an explicit request to continue.

Create a short record under `learning-records/` only when there is evidence: what the learner demonstrated, the prompt or experiment, observed result, remaining gap, and suggested review date. Do not record mere lesson delivery as demonstrated learning.

## Guided continuation

On `--continue`, read `MISSION.md`, `COURSE.md`, `PROGRESS.md`, the current layer's latest lesson, relevant sources, and any evidence record linked from progress. Choose exactly one action using this order:

1. **Clarify the mission** when a missing goal, target capability, or environment detail would materially change what “enough” means. Ask one compact question and stop.
2. **Evaluate a pending learner response** when the previous turn contains an answer, prediction, or experiment. Compare it with the layer's completion criterion; give focused feedback, update evidence and status, then stop. Do not add a new lesson in the same response.
3. **Review** when the current layer is `△`, has no evidence, or has a due review. Ask one retrieval, prediction, comparison, or diagnosis prompt without revealing the answer, then stop.
4. **Deepen or experiment** when the evidence exposes a misconception, relevant assumption, contradiction, or incomplete causal model. Address only that gap with one example or experiment, then stop.
5. **Advance** when the current layer meets the mission-adjusted completion criterion at `✓` or `◆`. Select the earliest applicable layer still `○`, normally the next numerical layer, and teach only that layer.
6. **Finish the current course pass** when every mission-relevant layer is `✓`, `◆`, or justified `N/A`. Report the achieved capabilities, remaining learning debt, and a recommended real-world project or review; do not invent another layer.

Never promote a status because the agent explained the material clearly or because the learner said only that they understood. If evidence is ambiguous, keep the status and ask a smaller discriminating question. Do not demand depth beyond the mission: record optional advanced gaps as learning debt and allow advancement.

`--continue` makes the pedagogical choice but does not run autonomously. It performs one action per invocation and then waits for the learner.

## Persist state

The workspace, not the conversation, is the durable memory. After a state-changing learning interaction, update the relevant files when the workspace is writable. `--save` forces an update; `--resume` reads it. Preserve user-authored notes. Keep `PROGRESS.md` concise and link to lessons and learning records instead of copying them.

If no workspace is writable, keep concise in-conversation state and say that cross-session continuation requires a saved record. Never claim cross-session memory solely from conversation history.

End each lesson with exactly one natural next action, normally `--review`, `--deepen`, or `--next`.
