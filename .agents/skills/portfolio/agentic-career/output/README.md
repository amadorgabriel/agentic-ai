# Career Output Root

Shared memory for all **Agentic Career** skills (`agentic-career` and children).

Path: `.agents/skills/portfolio/agentic-career/output/`

## Layout

| Path | Purpose |
| --- | --- |
| `experience/` | **Experience Memory** — Hybrid Artefacts (XYZ + STAR) per company/project. Written by `git-commits-to-cv` and by Phase 1 `append-data-to-cv` normalization. Migrated from `portfolio/.specs/`. Canonical for Consolidation / (Phase 2) adapt-cv-to-job. |
| `inbox/` | **Career Inbox** — raw uploads/pastes/JDs before normalization. See [inbox/README.md](./inbox/README.md). Gitignored (PII); only README tracked. |
| `cv/` | Working CV output. **Master CV** PT/EN: `master_cv.md` + `master_cv.en.md` (Phase 1 Consolidation). **Tailored CV**: `master_cv.<job-slug>.md` alongside Master (Phase 2 `adapt-cv-to-job`). See [cv/README.md](./cv/README.md). |
| `goals.md` | **Goals Artefact** — user-instance goals (target role(s), location prefs, comp floor, constraints, positioning hypotheses). Written by Phase 1 `goals-intake` Reference Module; Smart Merge on re-runs. Created when intake runs (path documented; file may be absent). |
| `linkedin/` | LinkedIn subtree — **LinkedIn Profile Snapshot** (`profile.md`) and **Post Ideas Artefact** (`post-ideas.md`). Phase 2 modules. See [linkedin/README.md](./linkedin/README.md). |
| `companies/` | **Company Shortlist** — BR (`br.md`) and LATAM (`latam.md`). Paths locked; real content filling = Phase 2. See [companies/README.md](./companies/README.md). |
| `study/` | **Study Plan** — single file `plan.md`. Path locked; full planning module = Phase 2. See [study/README.md](./study/README.md). |
| `applications.md` | Optional future **Applications Log** — Phase 2 deferred (path reserved; not required yet). |
| _(other)_ | Future: optional publish-cv — TBD |

**Phase 1 writers**: `goals-intake` → `goals.md`; `append-data-to-cv` → `inbox/` + `experience/`; `summarize-into-doc` → `cv/master_cv.md` + `cv/master_cv.en.md`; sibling `git-commits-to-cv` → `experience/`. Mother skill + references: [../SKILL.md](../SKILL.md), [../references/](../references/).

## Rules

- Do not scatter career artefacts outside this root without updating Career context.
- Do not treat scanned git repos as write targets for experience memory.
- Do not treat **Career Inbox** as Experience Memory; Consolidation reads `experience/` (+ Master CV). `adapt-cv-to-job` reads experience + Master from canonical paths and may read raw JD from inbox.
- Consolidation (`summarize-into-doc`, Phase 1) writes **Master CV** + **Master CV EN** at `cv/master_cv.md` and `cv/master_cv.en.md` (full dir: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\`). Never invent EN master content until Consolidation runs.
- `adapt-cv-to-job` (Phase 2) writes **Tailored CV** at `cv/master_cv.<job-slug>.md` alongside Master — **not** under `cv/tailored/`. Does not overwrite Master. Raw JD recommended default: **Career Inbox**. See Career Resolved decision 14 and [cv/README.md](./cv/README.md).
- Do **not** auto-update Portfolio CV (`c:\_git\projects\portfolio\public\assets\pdf\current_cv.md`); that sync is a separate explicit/manual step (future optional publish-cv).
- **Goals Artefact** path: `goals.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\goals.md`). Do not invent stub content before intake; do not put live goals into `context/career/CONTEXT.md`.
- **Personal data**: this entire `output/` tree is gitignored except `**/README.md` structure placeholders — do not commit goals, artefacts, masters, shortlists, or inbox dumps.
- **Goals Intake Gating (C)** when `goals.md` is absent: **Hard Gate** (must run intake / require file) for `adapt-cv-to-job` and `optimize-linkedin-profile`; **Soft Gate** (warn + offer intake; may continue on glossary defaults) for Consolidation / `summarize-into-doc`, `git-commits-to-cv`, `append-data-to-cv`, `linkedin-post-ideas`, and study planning.
- Hybrid Artefacts carry metadata **source**: `git` \| `manual` \| `cv-import` \| `doc` (see Career Resolved decision 12).
- **LinkedIn Profile Snapshot**: `linkedin/profile.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\profile.md`). Intake = paste/export → **Career Inbox** → normalize; no LinkedIn CLI/scraper as default. Do not invent full profile content before the user provides material.
- **Post Ideas Artefact**: `linkedin/post-ideas.md` (preferred path). Written by `linkedin-post-ideas` Reference Module.
- `optimize-linkedin-profile` (planned) reads Snapshot + Goals (**Hard Gate**); proposes only — never auto-posts to LinkedIn. See Career Resolved decision 13 and [context/linkedin/CONTEXT.md](../context/linkedin/CONTEXT.md).
- **Company Shortlist** (Decision A): `companies/br.md`, `companies/latam.md`. Recommended **Company Entry** fields: name, link, remote/hybrid tags, comp signal, stack, tier (`dream` \| `realistic` \| `stretch`). Do **not** research/fill real lists from path stubs — populate via agentic-career. See Career Resolved decision 15 and [companies/README.md](./companies/README.md).
- **Study Plan** (Decision A): `study/plan.md` — single plan from goals + recurring JD gaps / Tailored CV analyses. Study-planning = **Reference Module** under `agentic-career/references/` only. Do **not** invent full plan content from stubs. See [study/README.md](./study/README.md).
- **Applications Log** (`applications.md`) — optional future; unresolved/deferred.
