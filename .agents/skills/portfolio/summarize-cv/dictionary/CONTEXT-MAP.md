# Context Map — Summarize CV

Glossários de domínio da skill **`summarize-cv`**. Vivem em `.agents/skills/portfolio/summarize-cv/dictionary/`.

Dados do usuário (Summarize CV Output Root): `.agents/skills/portfolio/summarize-cv/output/` (gitignored).

Skills irmãs (portfolio): `git-commits-to-cv`, `optimize-linkedin`, `study-planning` — ver [README da categoria](../../README.md).

## Contexts (this skill)

- [CV](./cv/CONTEXT.md) — goals, inbox, experience memory, master/tailored CV, Pipeline A, adapt-cv-to-job

## Sibling dictionaries (not under this folder)

- [CV from Commits](../../git-commits-to-cv/dictionary/cv-from-commits/CONTEXT.md) — owned by `git-commits-to-cv`
- [LinkedIn](../../optimize-linkedin/dictionary/linkedin/CONTEXT.md) — owned by `optimize-linkedin`

## Relationships

- **summarize-cv** owns **Summarize CV Output Root** (`output/` with `goals.md`, `cv/`, `experience/`, `inbox/`)
- **git-commits-to-cv** writes Hybrid Artefacts into **Experience Memory** (`summarize-cv/output/experience/`); does not consolidate masters
- **Consolidation** (`summarize-into-doc`) → **Master CV** + **Master CV EN**
- **adapt-cv-to-job** (Reference Module) → **Tailored CV** alongside masters; JD from **Career Inbox**
- **optimize-linkedin** / **study-planning** may **read** `summarize-cv/output/**`; write only under their own `output/`
- LinkedIn / study requests are **not** executed inside `summarize-cv` — invoke the sibling skill

## Canonical paths

| Artefact | Path |
| --- | --- |
| Skill | `.agents/skills/portfolio/summarize-cv/` |
| Output root | `.agents/skills/portfolio/summarize-cv/output/` |
| Experience | `.../output/experience/` |
| Inbox | `.../output/inbox/` |
| Masters | `.../output/cv/master_cv.md`, `master_cv.en.md` |
| Tailored | `.../output/cv/master_cv.<job-slug>.md` |
| Goals | `.../output/goals.md` |
