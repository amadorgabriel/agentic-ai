---
name: agentic-career
description: >-
  Orchestrates career repositioning (CV, LinkedIn, study, applications) with
  shared memory under output/. Phase 1: CV Happy Path via reference modules
  (goals-intake, append-data-to-cv, summarize-into-doc) + sibling
  git-commits-to-cv. Use when the user explicitly invokes agentic-career,
  asks to otimizar currículo / optimize CV, or coordinate the career skill
  system as a whole.
disable-model-invocation: true
---

# Agentic Career

Mother skill for career repositioning. Orchestrates shared memory + **Real Child Skills** / **Reference Modules**.

Categoria: **career** — ver [README da categoria](../README.md).

**Phase 1 (shipped)** — CV pipeline references + this skill. **Phase 2 (deferred)** — LinkedIn optimize, adapt-cv-to-job, study/companies content, applications log, full linkedin-post-ideas. See [context/career/CONTEXT.md](context/career/CONTEXT.md) Resolved decision 18.

## Domain sources

Domain glossaries live under **`context/`** inside this skill (not the repo root):

- Context map: [context/CONTEXT-MAP.md](context/CONTEXT-MAP.md)
- Career context: [context/career/CONTEXT.md](context/career/CONTEXT.md)
- CV from commits: [context/cv-from-commits/CONTEXT.md](context/cv-from-commits/CONTEXT.md)
- LinkedIn: [context/linkedin/CONTEXT.md](context/linkedin/CONTEXT.md)

Future career grilling (`grill-with-docs`) updates `context/**` here — never recreate career glossaries at the `agentic-ai` repo root.

## When to use / routing (decision 17)

Only on **explicit** invoke (`disable-model-invocation: true`). Detect intent:

| Intent | Route | Behaviour |
| --- | --- | --- |
| Optimize / build / refresh CV (“otimizar currículo”, “optimize CV”, …) | **CV Happy Path** → **Pipeline A** | Ordered CV sequence; confirm before heavy steps |
| LinkedIn, study, companies, job-adapt, or unclear career ask | **Generic Invoke** → **Menu C** | Ask what to do; dispatch or point to Phase 2 stub |

Unclear intent → prefer **Menu C** (do not assume Pipeline A).

Orchestration detail → [references/cv-happy-path.md](references/cv-happy-path.md).

## Pipeline A — CV Happy Path

Skip steps already done / not applicable. Detail: [references/cv-happy-path.md](references/cv-happy-path.md).

1. **Goals** — if `output/goals.md` missing: **Soft Gate** → [references/goals-intake.md](references/goals-intake.md) (warn + offer; may continue on glossary defaults).
2. **Append** — if **Career Inbox** has items or user has materials → [references/append-data-to-cv.md](references/append-data-to-cv.md).
3. **Git → experience** — for missing/refresh repos: invoke sibling **`git-commits-to-cv`** at [`.agents/skills/portfolio/git-commits-to-cv/SKILL.md`](../git-commits-to-cv/SKILL.md). **User provides each Scanned repository path** (absolute). No filesystem auto-discovery. **Confirm before each git scan.**
4. **Consolidation** — [references/summarize-into-doc.md](references/summarize-into-doc.md) → **Master CV** `output/cv/master_cv.md` + **Master CV EN** `output/cv/master_cv.en.md`. **Confirm before rewriting masters.**

**Heavy-step Confirmation** — explicit user OK before:

- Starting `git-commits-to-cv` scan
- Rewriting Master / Master EN

**Never** write Portfolio CV (`portfolio/public/assets/pdf/current_cv.md`) from Consolidation.

## Menu C — Generic Invoke

1. Ask what the user wants.
2. Dispatch:

| Pedido | Destino Phase 1 |
| --- | --- |
| CV / master / consolidar / commits → experiência | Pipeline A ou módulo/skill correspondente abaixo |
| goals / objetivos | [references/goals-intake.md](references/goals-intake.md) |
| colar CV / docs / notes → memória | [references/append-data-to-cv.md](references/append-data-to-cv.md) |
| extrair de um repo git | sibling [git-commits-to-cv](../git-commits-to-cv/SKILL.md) (user dá path) |
| gerar/reescrever master CV | [references/summarize-into-doc.md](references/summarize-into-doc.md) |
| adaptar CV a uma vaga | **Phase 2** — `adapt-cv-to-job` (folder not created) |
| otimizar perfil LinkedIn | **Phase 2** — `optimize-linkedin-profile` |
| ideias de post LinkedIn | **Phase 2** — `linkedin-post-ideas` reference |
| study plan / company shortlist (preencher de verdade) | **Phase 2** — paths existem; content filling deferred |
| applications tracker | **Phase 2** — `applications.md` deferred |

3. Do **not** silently start **Pipeline A**.

## Shared memory (Career Output Root)

```
c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\
```

| Path | Role |
| --- | --- |
| `experience/` | **Experience Memory** — Hybrid Artefacts (PT-BR) |
| `inbox/` | **Career Inbox** — raw (gitignored); not canonical experience |
| `cv/master_cv.md` | **Master CV** (PT) — Consolidation only |
| `cv/master_cv.en.md` | **Master CV EN** — Consolidation only |
| `cv/master_cv.<job-slug>.md` | **Tailored CV** — Phase 2 (`adapt-cv-to-job`) |
| `goals.md` | **Goals Artefact** — goals-intake (Smart Merge) |
| `linkedin/` | Snapshot + post-ideas — Phase 2 modules |
| `companies/`, `study/` | Shortlists + study plan paths — content Phase 2 |

Layout detail → [output/README.md](./output/README.md).

## Goals Intake Gating (C)

When `output/goals.md` is missing:

| Gate | Behaviour | Applies to |
| --- | --- | --- |
| **Hard Gate** | Must run goals-intake / require `goals.md` before continuing | `adapt-cv-to-job`, `optimize-linkedin-profile` (**Phase 2**) |
| **Soft Gate** | Warn + offer intake; may continue with glossary defaults (Fullstack/Frontend Pleno, SP/híbrido-remoto/LATAM, >10k BRL) | Consolidation, `git-commits-to-cv`, `append-data-to-cv`, Pipeline A goals step; (Phase 2 also: linkedin-post-ideas, study-planning) |

## Packaging (hybrid)

| Kind | Status | Name | Role |
| --- | --- | --- | --- |
| Real Child Skill | Existing | [`git-commits-to-cv`](../git-commits-to-cv/SKILL.md) | Commits → Hybrid Artefacts (`source: git`). Invoke sibling skill; user provides repo path |
| Real Child Skill | Phase 2 | `optimize-linkedin-profile` | Folder not created — menu stub only |
| Real Child Skill | Phase 2 | `adapt-cv-to-job` | Folder not created — menu stub only |
| Reference Module | Phase 1 | [goals-intake](references/goals-intake.md) | → `output/goals.md` (Smart Merge) |
| Reference Module | Phase 1 | [append-data-to-cv](references/append-data-to-cv.md) | Inbox → Experience Memory (`manual`\|`cv-import`\|`doc`) |
| Reference Module | Phase 1 | [summarize-into-doc](references/summarize-into-doc.md) | Consolidation → dual masters; never Portfolio CV |
| Reference Module | Phase 1 helper | [cv-happy-path](references/cv-happy-path.md) | Orchestrates Pipeline A |
| Reference Module | Phase 2 | `linkedin-post-ideas`, study-planning, company-shortlist | Paths locked; full modules deferred |

## Invoking git-commits-to-cv

When Pipeline A (or Menu C) needs commit extraction:

1. Collect inputs required by the sibling skill (repo path, company-slug, project-slug, Commit Window, …).
2. Get **Heavy-step Confirmation**.
3. Follow [../git-commits-to-cv/SKILL.md](../git-commits-to-cv/SKILL.md) and its `references/` — do **not** reimplement commit clustering here.
4. Artefacts land in `output/experience/` with `source: git`.

## Hard rules

- Explicit invocation only (`disable-model-invocation: true`)
- Prefer `context/CONTEXT-MAP.md` + child contexts under `context/` over inventing terms
- Routing 17: CV-optimize → Pipeline A; else Menu C; unclear → Menu C
- Pipeline A: Soft Gate goals; append when needed; `git-commits-to-cv` only with **user-provided paths**; Consolidation → dual masters; **confirm before git scan and Master rewrite**
- Consolidation writes **only** `output/cv/master_cv.md` + `master_cv.en.md` — **never** `portfolio/.../current_cv.md`
- Consolidation reads `experience/` (+ goals soft) — never raw inbox as experience; artefacts stay PT-BR; EN only at Master EN
- Do **not** create `adapt-cv-to-job` / `optimize-linkedin-profile` skill folders in Phase 1
- Do **not** fill real company shortlists or invent full study/LinkedIn/applications content from stubs
- Hard Gate vs Soft Gate as table above (Phase 2 hard-gated skills: refuse to proceed without goals when those skills eventually run)
- Hybrid Artefact `source`: `git` (sibling skill) \| `manual` \| `cv-import` \| `doc` (append-data)

## References (Phase 1)

- [references/cv-happy-path.md](references/cv-happy-path.md) — Pipeline A orchestration
- [references/goals-intake.md](references/goals-intake.md) — Goals Artefact
- [references/append-data-to-cv.md](references/append-data-to-cv.md) — Inbox → experience
- [references/summarize-into-doc.md](references/summarize-into-doc.md) — Consolidation
- [../git-commits-to-cv/SKILL.md](../git-commits-to-cv/SKILL.md) — Real Child Skill (commits → artefacts)
