# CLAUDE.md — Statecraft Learning Wiki schema

This is the operating manual for this repository. It is a self-maintaining, LLM-built study system for political science and history, organized around the ruler's-eye question: how would a ruler actually govern a polity at a given time and place?

Two companion documents govern how you work and must be consulted:
- [statecraft-syllabus.md](statecraft-syllabus.md) — the spine. 12 units, 3 tiers, ordered by the sequence of ruling problems.
- [learning-science-for-self-study.md](learning-science-for-self-study.md) — the generation rulebook for study items and retrieval practice.
- [historical-epistemics.md](historical-epistemics.md) — the source-discipline and methods rulebook for contested historical claims.

> Terminology: the syllabus is organized into Units. The driving command is `create chapter X`, where "chapter X" == "Unit X". `create chapter`, `create unit`, and `do chapter` are synonyms.

---

## Directory layout

```
world-leader-undergrad/
├── CLAUDE.md
├── statecraft-syllabus.md
├── learning-science-for-self-study.md
├── historical-epistemics.md
├── course-map.md
├── index.md
├── coverage.md
├── log.md
├── research/
│   └── unitNN-<slug>-sources.md
├── wiki/
│   ├── unitNN-<slug>.md
│   ├── concept-<slug>.md
│   ├── theory-<slug>.md
│   ├── study-<slug>.md
│   ├── person-<slug>.md
│   ├── case-<slug>.md
│   ├── debate-<slug>.md
│   └── era-<slug>.md
├── items/
│   ├── unitNN-<slug>.md
│   ├── aux-<slug>.md
│   └── build/
│       └── items.json
├── apps/
├── docs/
└── review_log.csv
```

Empty directories carry a short README.md until populated.

---

## Storage decision (locked)

Markdown in items/ is the source of truth. The build step compiles items/*.md into items/build/items.json for the apps. Apps read items.json and write attempts to review_log.csv. Readings and items remain separate: the app reads compiled content and writes only scheduling state and attempts.

---

## The governing lens

The system is governed by one question: if I wanted to rule a nation at any point in history, how would I actually do it? Every unit, page, concept, and item must earn its place by answering a ruler's problem.

Every unit chapter page and every concept page must include a `## Across eras` section that explains how the problem looks in:
- a pre-state chiefdom
- an agrarian empire
- an early-modern composite monarchy
- an industrial nation-state
- a contemporary state

Each page must also mark what is invariant across eras and what specific technology or condition changed the problem.

Anachronism is a first-class error. If a mechanism is era-bound, say so explicitly.

---

## Page conventions (wiki/)

- One concept per page. Split if a page is doing two jobs.
- Write prose as continuous paragraphs, not hard-wrapped lines.
- YAML frontmatter on every page:

```yaml
---
title: State Capacity
type: concept
unit: 1
source_units: [1, 2]
cluster: state-capacity
---
```

- Use wikilinks for cross-references: `[[concept-state-capacity]]`.
- Every page needs a `## Sources` section with inline citations or source references.
- Every concept page and chapter page must include `## Across eras`.
- New page types:
  - `type: case` for case pages
  - `type: debate` for contested causal questions
  - `type: era` for era-environment pages

---

## Item conventions (items/)

Items live in one markdown file per unit or elective module. Each file contains one or more fenced ```json blocks, each a JSON array of item objects. The compiler extracts every json block and merges them.

Shape:

````
```json
[
  {
    "id": "u1-sovereignty-01",
    "prompt": "You inherit a fragile realm in 1500. Your army is loyal to your cousin, not to you. What do you do first?",
    "answer": "Secure your coalition and the army's loyalty before attempting broader reforms.",
    "type": "decision",
    "source_page": "wiki/concept-sovereignty.md",
    "topic": "state-formation",
    "cluster": "state-formation",
    "bloom_level": "analyze",
    "era": "early-modern"
  }
]
```
````

Field vocab:
- `type` ∈ cloze | recall | mcq | case | compare | explain | decision | counterfactual | attribution | forecast
- `bloom_level` ∈ remember | understand | apply | analyze | evaluate
- `era` is optional but required whenever the answer is era-bound.
- For `cloze`, write the blank as `{{...}}` in `prompt` and put the deleted text in `answer`.
- For `mcq`, add an `options` array and a `correct` field with the exact option string.

The apps assume the source_page exists and the item bank is valid JSON.

---

## Generate rules

Consult [learning-science-for-self-study.md](learning-science-for-self-study.md) before generating any items. For each major concept:
- span Bloom levels
- prefer production over recognition
- one idea per item
- keep the answer/feedback with the item
- cluster confusable concepts
- include compare-and-contrast items across theories and institutions
- generate decision, counterfactual, attribution, and forecast items for the ruler's-eye lens

---

## Research rules

- Triangulate with multiple independent sources.
- Prefer peer-reviewed work, university presses, and replicable datasets over think-tank or popular output.
- Cite everything non-obvious.
- Flag uncertainty, disagreement, and era-bound claims.
- Keep fact vs interpretation vs projection visibly distinct.
- For contested questions, create a debate page rather than smoothing the disagreement away.

---

## Ad-hoc / elective modules (`create module "<topic>"`)

Topics outside the 12-unit spine are built as elective modules in an `aux-<slug>` namespace so the spine remains stable.

---

## Apps rule

The apps read items/build/items.json and write attempts to review_log.csv. They never modify readings or item source. The phone app needs its own Supabase project or schema column if the statecraft repo is kept separate from the psychology repo.
