# CV (Summarize CV)

Domain context for the **summarize-cv** skill: goals, inbox, experience memory, master/tailored CVs, and CV pipeline orchestration. User memory lives under the **Summarize CV Output Root**.

Skill: `.agents/skills/portfolio/summarize-cv/`

**Docs home**: `.agents/skills/portfolio/summarize-cv/dictionary/` (see [CONTEXT-MAP.md](../CONTEXT-MAP.md)). Not at the `agentic-ai` repo root. Future CV grilling (`grill-with-docs`) updates `summarize-cv/dictionary/**` only.

Sibling skills (flat — no mother orchestrator): `git-commits-to-cv`, `optimize-linkedin`, `study-planning`.

## Language

### Orchestration & memory

**Summarize CV**:
The portfolio skill (`summarize-cv`) that runs the CV pipeline (goals → append → git experience → consolidation → job adapt) using **Reference Modules** and the sibling **`git-commits-to-cv`**. Does **not** execute LinkedIn or study work — redirect to sibling skills.
_Avoid_: Mother skill / Agentic Career umbrella, running LinkedIn or study inside this skill, treating every step as a standalone skill

**Summarize CV Output Root**:
Directory for this skill's user data: `.agents/skills/portfolio/summarize-cv/output/`. Contains `goals.md`, `cv/`, `experience/`, `inbox/` only.
_Avoid_: Career Output Root (old name), nesting `linkedin/` / `companies/` / `study/` here, scattering CV artefacts per skill without this root

**Experience Memory**:
Subtree holding Hybrid Artefacts: `output/experience/` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\experience\`). Canonical for Consolidation and job adaptation.
_Avoid_: `portfolio/.specs`, treating **Career Inbox** as Experience Memory

**Career Inbox**:
Raw landing zone: `output/inbox/` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\inbox\`). Uploads/pastes/notes **and** raw **Job Description**s. Personal files under the Output Root are gitignored (no README placeholders required).
_Avoid_: Writing Hybrid Artefacts here, reading inbox as canonical experience, committing raw dumps

**Artefact Source**:
Metadata `source` on a Hybrid Artefact: `git` (from `git-commits-to-cv`), or `manual` \| `cv-import` \| `doc` (from append-data).
_Avoid_: Omitting source, inventing alternate provenance labels

**Master CV**:
Canonical working CV (PT-BR): `output/cv/master_cv.md`. Written by **Consolidation**. Unchanged by `adapt-cv-to-job`.
_Avoid_: Treating **Portfolio CV** as working draft, overwriting Master when adapting

**Master CV EN**:
English master: `output/cv/master_cv.en.md`. Generated at Consolidation from PT-BR XYZ without rewriting Hybrid Artefacts.
_Avoid_: Rewriting artefacts into English, inventing EN master before Consolidation

**CV Language Policy (dual-track)**:
Hybrid Artefacts **PT-BR only**; Master PT + Master EN; each **Tailored CV** follows **Job Description** language (filename `master_cv.<job-slug>.md`). LinkedIn language lives in `optimize-linkedin` dictionary.
_Avoid_: Bilingual artefacts, dual tailored filenames per job

**Tailored CV**:
Job-specific variant: `output/cv/master_cv.<job-slug>.md`. Written by `adapt-cv-to-job` **Reference Module**. May link to inbox JD + embed **JD Summary**.
_Avoid_: `output/cv/tailored/`, overwriting masters

**Job Slug**:
Short kebab-case id for Tailored CV filename.
_Avoid_: Spaces, nested paths, long slugs

**Job Description**:
Raw JD material. Default landing zone: **Career Inbox**.
_Avoid_: Treating raw JD as Experience Memory

**JD Summary**:
Requirements summary embedded in a **Tailored CV** so `study-planning` can work without opening the inbox file.
_Avoid_: Dumping full raw JD into Experience Memory

**Portfolio CV**:
Published site CV: `c:\_git\projects\portfolio\public\assets\pdf\current_cv.md`. Not written by Consolidation.
_Avoid_: Using as Consolidation write target

**Consolidation**:
Reference module `summarize-into-doc` → Master CV + Master CV EN under `output/cv/`. No Portfolio sync.
_Avoid_: Auto-updating Portfolio CV

**publish-cv** (future optional):
Explicit Master → Portfolio sync. Out of Consolidation scope.
_Avoid_: Treating publish as part of `summarize-into-doc`

**Skill Packaging (flat siblings)**:
Heavy reusable work = sibling skills with own `SKILL.md`. Lightweight CV steps = **Reference Modules** under `summarize-cv/references/`. No mother skill.
_Avoid_: Mother skill packaging, inventing standalone skills for every lightweight CV step

**Reference Module**:
Lightweight step under `summarize-cv/references/`: goals-intake, `append-data-to-cv`, `summarize-into-doc`, `adapt-cv-to-job`, `cv-happy-path`.
_Avoid_: Creating skill folders for these; treating study/LinkedIn as modules inside summarize-cv

**append-data-to-cv**:
Reference Module: raw → **Career Inbox** → normalize into **Experience Memory** with source `manual` \| `cv-import` \| `doc`.
_Avoid_: Leaving normalized bullets only in inbox

**Goals Artefact**:
`output/goals.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\goals.md`). Written by goals-intake via **Smart Merge**.
_Avoid_: Putting live goals into this glossary, inventing stub before intake

**Goals Intake Gating**:
**Hard Gate** for `adapt-cv-to-job` and sibling `optimize-linkedin`. **Soft Gate** for Consolidation, `git-commits-to-cv`, `append-data-to-cv`, Pipeline A.
_Avoid_: All-hard or all-soft without updating this glossary

**Hard Gate**:
Must have `goals.md` / run intake before continuing.
_Avoid_: Soft-warning past hard-gated steps

**Soft Gate**:
Warn + offer intake; may continue on glossary defaults (**Target Role**, **Location Preference**, **Comp Floor**).
_Avoid_: Hard-blocking soft-gated steps

**CV Happy Path**:
Intent to optimize/build/refresh CV → **Pipeline A**.
_Avoid_: Treating LinkedIn/study asks as CV Happy Path

**Pipeline A**:
(1) goals if missing (**Soft Gate**); (2) append when inbox/materials; (3) `git-commits-to-cv` with user-provided paths; (4) Consolidation → dual masters. **Heavy-step Confirmation** before git scan and Master rewrite.
_Avoid_: Filesystem auto-discovery of repos, silent Master overwrite

**Heavy-step Confirmation**:
Explicit OK before git scan and Master rewrite.
_Avoid_: Silent scans/overwrites

### Sibling skills (pointers)

**git-commits-to-cv**:
Sibling skill — commits → Hybrid Artefacts in **Experience Memory**. Dictionary: [cv-from-commits](../../../git-commits-to-cv/dictionary/cv-from-commits/CONTEXT.md).
_Avoid_: Replacing with a reference-only module

**optimize-linkedin**:
Sibling skill — profile optimization + post-ideas mode. Owns its `output/` and dictionary. May **read** Summarize CV Output Root. Stub until implemented. See [linkedin CONTEXT](../../../optimize-linkedin/dictionary/linkedin/CONTEXT.md).
_Avoid_: Running LinkedIn work inside summarize-cv, old slug `optimize-linkedin-profile` as folder name

**study-planning**:
Sibling skill — **Company Shortlist** + **Study Plan**. Owns `study-planning/output/`. May read Summarize CV Output Root (goals, Tailored CV JD Summary). Stub until implemented.
_Avoid_: Nesting companies/study under summarize-cv/output

**adapt-cv-to-job**:
**Reference Module** (not a sibling skill folder). Reads language-appropriate master + Experience Memory + raw JD (inbox); writes **Tailored CV**. **Hard Gate** on goals.
_Avoid_: Shipping as a separate skill folder, writing under `cv/tailored/`

### Job plan defaults

**Target Role**:
Eng. Software Fullstack Pleno, Frontend Pleno, or closely related titles.
_Avoid_: Junior-only framing as default

**Location Preference**:
Híbrido/remoto SP, or exterior 100% HO with LATAM priority.
_Avoid_: On-site-only SP as the only option

**Comp Floor**:
>10k BRL/mês (or equivalent).
_Avoid_: Accepting below-floor as default plan

**Company Shortlist** / **Company Entry** / **Company Tier** / **Study Plan**:
Owned by **study-planning** (`study-planning/output/companies/`, `study-planning/output/study/plan.md`). Not under Summarize CV Output Root.
_Avoid_: Recreating these under summarize-cv/output

**Applications Log** (deferred):
Optional future tracker — unresolved; not required.

## Relationships

- **summarize-cv** owns **Summarize CV Output Root**; siblings may read it; only this skill (+ `git-commits-to-cv` for experience) writes CV/experience/inbox/goals
- **Consolidation** reads Experience Memory — not raw inbox
- **adapt-cv-to-job** writes Tailored CV alongside masters; embeds **JD Summary** for study-planning
- LinkedIn / study asks → invoke sibling skills; do not Menu-dispatch execution inside summarize-cv
- Soft-gated steps may use glossary defaults; hard-gated steps must not

## Example dialogue

> **Dev:** "Where do Hybrid Artefacts live?"
> **Domain expert:** "**Experience Memory** under **Summarize CV Output Root** — `summarize-cv/output/experience/`."
>
> **Dev:** "Is there still a mother skill for LinkedIn and study?"
> **Domain expert:** "No. Flat siblings: `summarize-cv`, `git-commits-to-cv`, `optimize-linkedin`, `study-planning`."
>
> **Dev:** "Does Consolidation update portfolio `current_cv.md`?"
> **Domain expert:** "No. Only `master_cv.md` + `master_cv.en.md`. Portfolio sync is optional **publish-cv**."
>
> **Dev:** "User asks for LinkedIn help while in summarize-cv?"
> **Domain expert:** "Do not execute. Tell them to invoke `optimize-linkedin`."
>
> **Dev:** "Where does adapt write, and where is the JD?"
> **Domain expert:** "`output/cv/master_cv.<job-slug>.md`. Raw JD in **Career Inbox**. Embed **JD Summary** in the Tailored CV."

## Flagged ambiguities

- Exact Tailored CV selection/rewrite heuristics beyond v1 adapt module — refine with use
- **publish-cv** internals — unresolved
- **Applications Log** — deferred
- Who normalizes LinkedIn inbox → Snapshot — owned by `optimize-linkedin` (unresolved internals)

## Resolved decisions

1. ~~Mother skill = agentic-career~~ → **superseded by decision 19**: flat siblings; CV skill = `summarize-cv`.
2. **Docs layout** = `dictionary/CONTEXT-MAP.md` + domain folders under each skill (not repo root).
3. **Summarize CV Output Root** = `.agents/skills/portfolio/summarize-cv/output/`; Experience Memory = `output/experience/`. Personal outputs gitignored (no README requirement).
4. **Target roles** = Fullstack Pleno / Frontend Pleno / correlatos.
5. **Location** = híbrido/remoto SP, or exterior 100% HO LATAM priority.
6. **Comp floor** = >10k BRL/mês.
7. **Portfolio `.specs` cleanup** = Experience Memory sole canonical path under summarize-cv output.
8. **Packaging** = flat siblings + Reference Modules under `summarize-cv/references/` (includes `adapt-cv-to-job`). LinkedIn/study are sibling skills, not mother modules.
9. **Consolidation output = B** — masters under `output/cv/` only; no auto Portfolio update.
10. **Goals intake = A** — single `output/goals.md`; Smart Merge.
11. **Goals Intake Gating = C** — Hard: adapt + optimize-linkedin; Soft: consolidation / git / append / Pipeline A.
12. **append-data storage = B** — inbox + normalize to experience.
13. **LinkedIn** — owned by `optimize-linkedin` (see that dictionary). Cross-read summarize-cv output allowed.
14. **adapt-cv-to-job output = B** — `master_cv.<job-slug>.md` alongside Master; JD in Career Inbox. Implemented as Reference Module (decision 19).
15. **Companies + study** — owned by `study-planning` (`output/companies/br.md`, `latam.md`, `output/study/plan.md`).
16. **CV language = B (dual-track)** — artefacts PT-BR; dual masters; tailored = JD language.
17. **Routing** — CV optimize → Pipeline A; adapt → adapt module; LinkedIn/study → redirect to siblings (no Menu C orchestration of siblings).
18. **Phase 1 history** — CV pipeline reference modules shipped under former `agentic-career`.
19. **Redesign grill 2026-08-06 (grill-with-docs)** — user decisions Q1–Q20:
    - Rename `agentic-career` → `summarize-cv`; `context/` → `dictionary/`; `career/` → `cv/`
    - Flat siblings; no mother
    - Full Pipeline A + adapt in-scope; adapt = `references/adapt-cv-to-job.md`
    - `study-planning` stub owns companies+study outputs
    - `optimize-linkedin` stub owns LinkedIn dictionary + output (profile + post-ideas mode)
    - `cv-from-commits` dictionary → `git-commits-to-cv/dictionary/`
    - JD in same inbox; cross-skill read of summarize-cv/output; no nested output READMEs
    - Vocabulary: **Summarize CV Output Root**; remove Mother / Agentic Career as live terms
