# CV output

Subtree of **Career Output Root** for working and job-adapted CV markdown.

Path: `.agents/skills/portfolio/agentic-career/output/cv/`

## Canonical paths

| Path | Artefact | Role |
| --- | --- | --- |
| `master_cv.md` | **Master CV** | Canonical working CV (PT-BR). Written by Consolidation (`summarize-into-doc`). Full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.md` |
| `master_cv.en.md` | **Master CV EN** | English master. Generated at Consolidation from PT-BR XYZ (without rewriting Hybrid Artefacts). Full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.en.md` |
| `master_cv.<job-slug>.md` | **Tailored CV** | Job-specific variant written by `adapt-cv-to-job`. Lives **alongside** masters — not under a `tailored/` subdirectory. Content language = JD language. |

## Naming (adapt output = Decision B)

- **Job Slug**: short kebab-case from company+role, or user-provided (e.g. `acme-fullstack-pleno` → `master_cv.acme-fullstack-pleno.md`).
- Do **not** create `cv/tailored/` or nest by company folder here.
- Do **not** overwrite `master_cv.md` or `master_cv.en.md` when adapting to a job.

## Language (dual-track = Decision B)

- Hybrid Artefacts / `git-commits-to-cv` stay **PT-BR only**.
- Masters: PT = `master_cv.md`; EN = `master_cv.en.md` (Consolidation may translate XYZ → EN master).
- **Tailored CV**: one file per job; language follows the **Job Description** (EN JD → EN content). Filename stays `master_cv.<job-slug>.md` — no separate `.en` suffix unless a later rule requires it.
- Do **not** invent `master_cv.en.md` content from this README alone — file appears when Consolidation runs.

## Job Description input

Recommended default (user did not explicitly pick otherwise):

1. Land raw **Job Description** in **Career Inbox**: `../inbox/`.
2. `adapt-cv-to-job` reads the language-appropriate master + Experience Memory + that JD.
3. Write **Tailored CV** here in the JD's language; optionally add frontmatter/link pointing to the inbox JD file.
4. Embed a **JD Summary** / requirements-extracted section in the Tailored CV so study-planning can work without opening the inbox.

Do **not** invent sample Tailored CV files from this README alone. Paths are documented; masters appear when Phase 1 Consolidation (`summarize-into-doc`) runs; tailored files wait for Phase 2 `adapt-cv-to-job`.

## Related

- Career context: [context/career/CONTEXT.md](../../context/career/CONTEXT.md) (Resolved decisions 9, 14, 16)
- Career Inbox: [../inbox/README.md](../inbox/README.md)
- Output root: [../README.md](../README.md)
