# Persistent course workspace

Store the course under the user's current workspace:

```text
learning-notes/<technology-slug>/
├── MISSION.md
├── RESOURCES.md
├── COURSE.md
├── PROGRESS.md
├── NOTES.md
├── lessons/
│   └── 001-layer-01-<slug>.md
├── reference/
│   └── <reusable-topic>.md
└── learning-records/
    └── YYYY-MM-DD-layer-N.md
```

The directory is the durable course. The conversation is where teaching happens.

## `MISSION.md`

Preserve why the learner began and the context at the time:

```markdown
# Mission: <technology>

- Started:
- Real task or reason:
- Prior knowledge:
- Target capability:
- Environment and constraints:
- Preferred teaching adjustments:
- Unknowns about the learner:

## Mission history

- YYYY-MM-DD — Initial mission established.
```

When the goal changes, update the current fields and append a dated history entry. Do not erase the original reason.

## `RESOURCES.md`

```markdown
# Sources: <technology>

| Source | Kind | Layers | Why trusted | Checked | Status |
| --- | --- | --- | --- | --- | --- |
| [Title](URL) | Official docs/spec/source/paper/community | 1, 2 | Maintained by ... | YYYY-MM-DD | Primary/Supporting/Unverified |
```

Record only consulted sources. Community sources can support judgement or field practice but must not be mislabeled as primary.

## `COURSE.md`

This is the human-facing table of contents:

```markdown
# Course: <technology>

## Purpose

One-paragraph summary linked to [MISSION.md](MISSION.md).

## Lessons

| No. | Date | Layer | Lesson | Outcome at the time | Status |
| ---: | --- | ---: | --- | --- | :---: |

## Reusable references

- [Title](reference/file.md) — purpose

## Learning evidence

- [Date — layer N](learning-records/file.md) — demonstrated capability

## Continue

- Current layer:
- Why this is the current layer:
- Next action:
```

Update it whenever a lesson, reusable reference, or evidence record is created.

## `PROGRESS.md`

```markdown
# Progress: <technology>

- Current layer:
- Last updated:
- Next action:
- Reason for next action:
- Review due:

| Layer | Name | Status | Latest lesson | Evidence | Open point |
| ---: | --- | :---: | --- | --- | --- |
| 1 | Identity and purpose | ○ | — | — | — |
...
| 20 | Independent explanation and application | ○ | — | — | — |

## Verified observations

## Assumptions

## Open questions

## Learning debt
```

Always include all 20 rows using the names in `observation-map.md`.

The `Next action` and `Reason for next action` fields are the persisted decision used by `--continue`. Re-evaluate them against current evidence rather than following a stale recommendation blindly.

## `NOTES.md`

Reserve this file for the learner's own remarks and teaching preferences. The skill may append an explicitly stated preference, but must not rewrite or reorganize user-authored notes without a request.

## Lesson

Use a sequence number so chronology remains visible:

```markdown
# <Technology> — Layer <N>: <title>

- Lesson: 001
- Date:
- Mission at this time:
- Status after delivery: △

## Why this matters
## Explanation
## Concrete example
## Observation questions
## Exercise or prediction
## Completion criterion
## Known facts, assumptions, and open question
## Sources
## Next action
## Corrections
```

A lesson is a historical artifact. Do not silently change its original teaching context. Append a dated correction, or create a new lesson that supersedes it. Lesson delivery alone receives `△`.

## Reusable reference

Create `reference/` files only for material worth revisiting, such as a glossary, command table, architecture diagram, troubleshooting sequence, or comparison guide. Link each one from `COURSE.md`. Keep the canonical explanation in one place.

## Evidence record

Create a record only after retrieval or an experiment:

```markdown
# Learning record: <technology> — layer <N>

- Date:
- Capability tested:
- Prompt or experiment:
- Learner's prediction or explanation:
- Observed result:
- What this demonstrates:
- Remaining gap:
- Status awarded:
- Suggested review date:
```

Keep it factual. A polished answer copied from the lesson does not itself demonstrate retrieval.

## Legacy migration

If `learning-notes/<technology-slug>.md` exists, read it and populate the course workspace without discarding facts, questions, dates, or learner wording. Leave the legacy file in place unless the user explicitly asks to remove or archive it. Note the migrated source in `PROGRESS.md` and `COURSE.md`.
