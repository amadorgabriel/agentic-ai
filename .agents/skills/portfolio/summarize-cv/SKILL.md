---
name: summarize-cv
description: >-
  Builds and maintains CV memory (inbox → experience → master CV PT/EN) and
  adapts the master to a specific job (Tailored CV). Orchestrates reference
  modules plus sibling git-commits-to-cv. Use when the user explicitly invokes
  summarize-cv, asks to otimizar currículo / optimize CV, adapt CV to a job,
  or consolidate experience into master CV.
disable-model-invocation: true
---

# Summarize CV

CV pipeline skill: goals → append → git experience → consolidation → job adapt.

Categoria: **portfolio** — ver [README da categoria](../README.md).

Sibling skills (invoke separately; do **not** run their work here):

- [`git-commits-to-cv`](../git-commits-to-cv/SKILL.md) — commits → Experience Memory
- [`cv-md-to-docx`](../cv-md-to-docx/SKILL.md) — Master/Tailored MD → Word `.docx` pronto para envio
- [`optimize-linkedin`](_/optimize-linkedin/SKILL.md), [`study-planning`](_/study-planning/SKILL.md) — stubs locais em `portfolio/_/` (gitignored; não versionados)

## Domain sources

Glossaries live under **`dictionary/`**:

- Map: [dictionary/CONTEXT-MAP.md](dictionary/CONTEXT-MAP.md)
- CV domain: [dictionary/cv/CONTEXT.md](dictionary/cv/CONTEXT.md)

`git-commits-to-cv` owns [../git-commits-to-cv/dictionary/cv-from-commits/CONTEXT.md](../git-commits-to-cv/dictionary/cv-from-commits/CONTEXT.md).

Future CV grilling (`grill-with-docs`) updates `summarize-cv/dictionary/**` — never recreate career glossaries at the `agentic-ai` repo root.

## When to use / routing

Only on **explicit** invoke (`disable-model-invocation: true`).

| Intent | Route |
| --- | --- |
| Optimize / build / refresh CV | **CV Happy Path** → **Pipeline A** |
| Adapt CV to a job / JD | **adapt-cv-to-job** → [references/adapt-cv-to-job.md](references/adapt-cv-to-job.md) |
| Export CV to Word / DOCX | **Do not execute here** — invoke sibling [`cv-md-to-docx`](../cv-md-to-docx/SKILL.md) |
| goals / append / consolidate / git extract (explicit) | Matching reference module or sibling skill |
| LinkedIn / study / companies | **Do not execute here** — tell user to invoke local stubs under `portfolio/_/` |
| Unclear | Ask what they want (CV path only); do **not** assume Pipeline A |

Orchestration detail → [references/cv-happy-path.md](references/cv-happy-path.md).

## Pipeline A — CV Happy Path

Skip steps already done / not applicable. Detail: [references/cv-happy-path.md](references/cv-happy-path.md).

1. **Goals** — if `output/goals.md` missing: **Soft Gate** → [references/goals-intake.md](references/goals-intake.md).
2. **Append** — if **Career Inbox** has items or user has materials → [references/append-data-to-cv.md](references/append-data-to-cv.md).
3. **Git → experience** — sibling **`git-commits-to-cv`**. User provides each repo path. **Confirm before each git scan.**
4. **Consolidation** — [references/summarize-into-doc.md](references/summarize-into-doc.md) → Master CV PT + EN. **Confirm before rewriting masters.**

**Heavy-step Confirmation** before: git scan; Master rewrite.

**Never** write Portfolio CV (`portfolio/public/assets/pdf/current_cv.md`) from Consolidation.

## adapt-cv-to-job

[references/adapt-cv-to-job.md](references/adapt-cv-to-job.md):

- **Hard Gate** on `output/goals.md`
- Raw JD → **Career Inbox** (same `inbox/` as other raw inputs)
- Writes `output/cv/master_cv.<job-slug>.md` — does **not** overwrite masters

## Summarize CV Output Root

```
.agents/skills/portfolio/summarize-cv/output/
```

| Path | Role |
| --- | --- |
| `experience/` | **Experience Memory** — Hybrid Artefacts (PT-BR) |
| `inbox/` | **Career Inbox** — raw (gitignored); includes JDs |
| `cv/master_cv.md` | **Master CV** (PT) |
| `cv/master_cv.en.md` | **Master CV EN** |
| `cv/master_cv.<job-slug>.md` | **Tailored CV** |
| `cv/confirmed_metrics.md` | **Confirmed Metrics Ledger** — fonte de verdade de números (CV PT, `cv-import`) |
| `cv/master_cv*.docx` | Word export via sibling [`cv-md-to-docx`](../cv-md-to-docx/SKILL.md) (gitignored) |
| `goals.md` | **Goals Artefact** (Smart Merge) |

No `linkedin/`, `companies/`, or `study/` here — those belong to sibling skills.

## Goals Intake Gating

When `output/goals.md` is missing:

| Gate | Behaviour | Applies to |
| --- | --- | --- |
| **Hard Gate** | Must run goals-intake / require `goals.md` | `adapt-cv-to-job`; sibling `optimize-linkedin` (when implemented) |
| **Soft Gate** | Warn + offer intake; may continue on glossary defaults | Consolidation, `git-commits-to-cv`, `append-data-to-cv`, Pipeline A goals step |

## Packaging

| Kind | Name | Role |
| --- | --- | --- |
| Sibling skill | [`git-commits-to-cv`](../git-commits-to-cv/SKILL.md) | Commits → Hybrid Artefacts (`source: git`) |
| Sibling skill | [`cv-md-to-docx`](../cv-md-to-docx/SKILL.md) | MD masters/tailored → `.docx` |
| Sibling skill (local) | `portfolio/_/optimize-linkedin` | LinkedIn (stub, gitignored) |
| Sibling skill (local) | `portfolio/_/study-planning` | Study + companies (stub, gitignored) |
| Reference | [goals-intake](references/goals-intake.md) | → `output/goals.md` |
| Reference | [append-data-to-cv](references/append-data-to-cv.md) | Inbox → experience |
| Reference | [summarize-into-doc](references/summarize-into-doc.md) | Consolidation → dual masters |
| Reference | [adapt-cv-to-job](references/adapt-cv-to-job.md) | Master + JD → Tailored CV |
| Reference | [cv-happy-path](references/cv-happy-path.md) | Pipeline A orchestration |

## Hard rules

- Explicit invocation only
- Prefer `dictionary/` glossaries over inventing terms
- Resolve every metric (Y) via the **Confirmed Metrics Ledger** (`output/cv/confirmed_metrics.md`) — it wins over artefact notes on conflicts; never invent a number
- LinkedIn / study / companies → redirect to sibling skills; do not execute here
- Pipeline A: Soft Gate goals; user-provided git paths; confirm before git scan and Master rewrite
- Consolidation writes **only** `master_cv.md` + `master_cv.en.md` — never Portfolio CV
- Consolidation reads `experience/` (+ goals soft) — never raw inbox as experience
- Hybrid Artefact `source`: `git` \| `manual` \| `cv-import` \| `doc`

## References

- [references/cv-happy-path.md](references/cv-happy-path.md)
- [references/goals-intake.md](references/goals-intake.md)
- [references/append-data-to-cv.md](references/append-data-to-cv.md)
- [references/summarize-into-doc.md](references/summarize-into-doc.md)
- [references/adapt-cv-to-job.md](references/adapt-cv-to-job.md)
- [../git-commits-to-cv/SKILL.md](../git-commits-to-cv/SKILL.md)
- [../cv-md-to-docx/SKILL.md](../cv-md-to-docx/SKILL.md)
