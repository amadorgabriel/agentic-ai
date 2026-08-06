# Career

Domain context for career repositioning: target roles, location/comp preferences, and the mother skill that orchestrates CV, LinkedIn, study, and job applications. Shared user memory lives under the Career Output Root.

Skill-mãe: `.agents/skills/portfolio/agentic-career/`

**Docs home**: this file and siblings live under `.agents/skills/portfolio/agentic-career/context/` (with [CONTEXT-MAP.md](../CONTEXT-MAP.md)). They are **not** at the `agentic-ai` repo root. Future career grilling (`grill-with-docs`) updates `agentic-career/context/**` only — do not recreate root-level `career/`, `cv-from-commits/`, `linkedin/`, or root `CONTEXT-MAP.md`.

## Language

### Orchestration & memory

**Agentic Career**:
The mother skill (`agentic-career`) that orchestrates career repositioning across CV, LinkedIn, study, and applications — with shared memory under **Career Output Root**. Invokes or points to **Real Child Skills**; keeps lightweight steps as **Reference Modules**.
_Avoid_: Loose collection of unrelated CV scripts, one-off portfolio-only workflow, treating every step as a standalone skill

**Career Output Root**:
Directory for all shared career-skill user data: `.agents/skills/portfolio/agentic-career/output/`.
_Avoid_: `portfolio/.specs`, scanned repo root, scattering artefacts per skill without a shared root

**Experience Memory**:
Subtree of **Career Output Root** holding Hybrid Artefacts of work experience: `output/experience/` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\`). Former Portfolio Memory Root under `portfolio/.specs/`. Canonical store for Consolidation and job adaptation — not the raw landing zone.
_Avoid_: Portfolio Memory Root, `portfolio/.specs`, writing experience next to **Master CV** or **Portfolio CV** by default, treating **Career Inbox** as Experience Memory

**Career Inbox**:
Raw landing zone under **Career Output Root** for uploads/pastes before normalization: `output/inbox/` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\inbox\`). Written by the user (or drop step); read by `append-data-to-cv` normalization. Also recommended default for raw **Job Description** input to `adapt-cv-to-job`. All personal files under **Career Output Root** are gitignored; only `output/**/README.md` structure placeholders stay tracked.
_Avoid_: Writing Hybrid Artefacts here, reading inbox as canonical experience for Consolidation / `adapt-cv-to-job`, committing raw inbox dumps or other personal output

**Artefact Source**:
Metadata field `source` on a Hybrid Artefact indicating provenance: `git` (from `git-commits-to-cv`), or from append-data normalization — `manual` \| `cv-import` \| `doc`. Aligns with the Hybrid Artefact template.
_Avoid_: Omitting source on new artefacts, inventing alternate provenance labels without updating this glossary

**Master CV**:
Canonical working CV in Brazilian Portuguese under **Career Output Root**: `output/cv/master_cv.md` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.md`). Written by **Consolidation** (`summarize-into-doc`). Unchanged by `adapt-cv-to-job`. Pair with **Master CV EN** under dual-track language policy.
_Avoid_: Treating **Portfolio CV** as the working draft, writing Consolidation output under `portfolio/`, inventing alternate working-CV filenames without updating this glossary, overwriting Master when adapting to a job, treating the PT file as the only Consolidation output when EN is also required

**Master CV EN**:
English counterpart of **Master CV** under **Career Output Root**: `output/cv/master_cv.en.md` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.en.md`). Generated at **Consolidation** (`summarize-into-doc`) by translating/adapting **XYZ Bullets** from PT-BR **Experience Memory** — without rewriting Hybrid Artefacts. Not created until Consolidation runs.
_Avoid_: Rewriting Hybrid Artefacts into English, bilingual sections inside artefacts, inventing EN master content before Consolidation, requiring a separate `.en` suffix on **Tailored CV** filenames

**CV Language Policy (dual-track)**:
Language model for CV/LinkedIn under **Agentic Career** (Decision B): Hybrid Artefacts stay **PT-BR only**; **Master CV** is PT (`master_cv.md`); **Master CV EN** is generated at Consolidation (`master_cv.en.md`); each **Tailored CV** is one file whose content language follows the **Job Description** language (filename stays `master_cv.<job-slug>.md`); LinkedIn profile optimization uses the primary language of the existing **LinkedIn Profile Snapshot**; LinkedIn **Post Ideas Artefact** may become bilingual later.
_Avoid_: Changing `git-commits-to-cv` / artefact language to bilingual, dual tailored filenames (`.md` + `.en.md`) per job, forcing EN into Experience Memory

**Tailored CV**:
Job-specific CV variant written by `adapt-cv-to-job`, living **alongside** **Master CV** in the same folder: `output/cv/master_cv.<job-slug>.md` (full path pattern: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.<job-slug>.md`). Not a `tailored/` subdirectory. Content language = **Job Description** language (PT or EN); one file per job — no separate `.en` filename unless naming rules change later. May include optional frontmatter/link to the raw **Job Description** in **Career Inbox**, plus an embedded **JD Summary** section.
_Avoid_: `output/cv/tailored/`, overwriting **Master CV**, scattering tailored files outside `output/cv/`, inventing alternate naming without updating this glossary, dual files per job for language

**Job Slug**:
Short kebab-case identifier from company+role or user-provided, used in the **Tailored CV** filename (`master_cv.<job-slug>.md`).
_Avoid_: Spaces, nested paths, long verbose slugs, using the slug as a subdirectory under `cv/`

**Job Description**:
Raw job-description material for a target application. Recommended default landing zone: **Career Inbox** (aligned with `append-data-to-cv`). User did not explicitly pick an alternate JD location — use this recommended default. Optional pointer from **Tailored CV** frontmatter/link to the inbox file.
_Avoid_: Treating raw JD as **Experience Memory**, inventing a separate JD root without updating this glossary, requiring inbox open when **JD Summary** is already in the Tailored CV

**JD Summary**:
Extracted requirements / JD summary section embedded in a **Tailored CV** so study-planning and related steps can work without opening the inbox file.
_Avoid_: Dumping the full raw JD into Experience Memory, omitting a usable summary when study-planning needs JD signal

**Portfolio CV**:
Published CV markdown in the portfolio site: `c:\_git\projects\portfolio\public\assets\pdf\current_cv.md`. Distinct from **Master CV**; not written by **Consolidation**.
_Avoid_: `current_cv.md` as the Consolidation write target, conflating with **Master CV**

**Consolidation**:
Reference-module step (`summarize-into-doc`) that merges **XYZ Bullets** from **Experience Memory** into the **Master CV** (PT) and may generate **Master CV EN** from the same PT-BR XYZ sources without rewriting Hybrid Artefacts. Writes only under `output/cv/`; does not sync to **Portfolio CV**.
_Avoid_: Auto-updating **Portfolio CV**, writing Consolidation under `portfolio/`, consolidating STAR Notes by default, translating artefacts in place to produce the EN master

**publish-cv** (future optional):
Possible later explicit/manual step to sync **Master CV** → **Portfolio CV**. Out of **Consolidation** scope for now.
_Avoid_: Treating publish as part of `summarize-into-doc`, auto-publish after Consolidation

**Skill Packaging (hybrid)**:
Packaging model for **Agentic Career**: heavy/reusable work is a **Real Child Skill**; lightweight orchestration stays as **Reference Modules** under `agentic-career/references/`. Supersedes any earlier "B — all under mother references only".
_Avoid_: B-only references packaging, inventing standalone skills for every lightweight step

**Real Child Skill**:
A standalone, invocável skill (own `SKILL.md`) for heavy or reusable-alone work under the **Agentic Career** umbrella. Canonical set: `git-commits-to-cv` (exists), `optimize-linkedin-profile` (planned), `adapt-cv-to-job` (planned).
_Avoid_: otimize-linkedin-profile, summaryze-into-doc as a skill name, treating reference-only modules as Real Child Skills

**Reference Module**:
A lightweight step documented only under `agentic-career/references/` (not a standalone skill): user-goals / goals-intake (writes **Goals Artefact**), `append-data-to-cv` (inbox → normalize → **Experience Memory**), `summarize-into-doc` (**Consolidation** → **Master CV** + optional **Master CV EN**), `linkedin-post-ideas` (Snapshot + goals + Master CV/experience → **Post Ideas Artefact**), study-planning (writes **Study Plan**), company-shortlist curation (writes **Company Shortlist** files), and other thin orchestration.
_Avoid_: Creating `.agents/skills/<name>/` folders for these, summaryze (typo), treating them as independently invocável root skills, inventing a standalone `study-planning` skill

**LinkedIn Profile Snapshot**:
Normalized current LinkedIn profile markdown under **Career Output Root**: `output/linkedin/profile.md`. From user paste/export via **Career Inbox** — not CLI/scraper by default. Full definition: [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
_Avoid_: Scraping LinkedIn as default, treating raw inbox as canonical profile

**Post Ideas Artefact**:
Preferred LinkedIn post-ideas file: `output/linkedin/post-ideas.md`. Written by `linkedin-post-ideas`. Full definition: [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
_Avoid_: Scattering post ideas outside `output/linkedin/`, auto-publishing to LinkedIn

**append-data-to-cv**:
**Reference Module** (Phase 1) that lands raw material in **Career Inbox**, then normalizes into/updates Hybrid Artefacts under **Experience Memory** with **Artefact Source** `manual` \| `cv-import` \| `doc`. Workflow: `agentic-career/references/append-data-to-cv.md`.
_Avoid_: Writing normalized bullets only in inbox, treating append as a Real Child Skill, skipping normalization into `experience/`

**Goals Artefact**:
Single user-instance file under **Career Output Root**: `output/goals.md` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\goals.md`). Holds target role(s), location prefs, comp floor, constraints, and positioning hypotheses. Written/updated by the user-goals / goals-intake **Reference Module** via **Smart Merge** on re-runs (preserve confirmed answers; merge new). Not domain glossary in this file.
_Avoid_: Putting goals into `career/CONTEXT.md`, scattering goals across multiple files, inventing alternate filenames without updating this glossary, creating stub content before intake runs

**Goals Intake Gating**:
Policy for when missing **Goals Artefact** blocks or only warns before a career step continues. Option C: **Hard Gate** for job/profile adaptation skills; **Soft Gate** for consolidation, extraction, append, posts, and study.
_Avoid_: Treating all steps as hard-required, treating all steps as soft-only, inventing a third gating mode without updating this glossary

**Hard Gate**:
Must run user-goals / goals-intake (or require existing `goals.md`) before continuing. Applies to: `adapt-cv-to-job`, `optimize-linkedin-profile`.
_Avoid_: Soft-warning past these skills without goals, inventing alternate hard-gated slugs without updating this glossary

**Soft Gate**:
Warn and offer intake when **Goals Artefact** is absent; may continue using glossary defaults (**Target Role**, **Location Preference**, **Comp Floor**). Applies to: **Consolidation** / `summarize-into-doc`, `git-commits-to-cv`, `append-data-to-cv`, `linkedin-post-ideas`, study-planning modules.
_Avoid_: Hard-blocking these steps on missing goals, skipping the warn/offer when goals are absent

**Child skill**:
Alias for **Real Child Skill** when contrasting with the mother. Full planned Real Child Skill list: `git-commits-to-cv`, `optimize-linkedin-profile`, `adapt-cv-to-job`.
_Avoid_: Treating every career task as a standalone root skill with no shared memory

**Mother Routing**:
How **Agentic Career** chooses work on invoke: intent detection → either **CV Happy Path** (**Pipeline A**) or **Generic Invoke** (**Menu C**). Locked by Resolved decision 17.
_Avoid_: Always running the full CV pipeline on any career ask, inventing alternate lettered pipelines without updating this glossary

**CV Happy Path**:
Intent to optimize / build / refresh the CV (e.g. "otimizar currículo", "optimize CV"). Runs **Pipeline A** under **Agentic Career**.
_Avoid_: Treating LinkedIn-only or study-only asks as CV Happy Path, skipping confirmation before heavy steps

**Pipeline A**:
Ordered CV-optimization sequence for **CV Happy Path**: (1) goals intake if missing (**Soft Gate** on this path); (2) `append-data-to-cv` when **Career Inbox** has items or the user has materials; (3) `git-commits-to-cv` for missing repos — **user provides each Scanned repository path** (no filesystem auto-discovery; matches existing skill; adopted as recommended default); (4) `summarize-into-doc` → **Master CV** + **Master CV EN**. Confirm before git scan and before rewriting Master.
_Avoid_: Auto-discovering repos on disk, running git scan or Master rewrite without confirmation, hard-blocking the whole path on missing goals

**Generic Invoke**:
Non-CV-happy-path invoke of **Agentic Career** (e.g. LinkedIn help, study, companies). Dispatches via **Menu C**.
_Avoid_: Silently starting **Pipeline A** on vague career asks

**Menu C**:
Dispatch mode for **Generic Invoke**: ask what the user wants to do, then route to the matching **Real Child Skill** or **Reference Module**.
_Avoid_: Assuming CV optimization, presenting an empty menu with no dispatch

**Heavy-step Confirmation**:
Explicit user confirmation required before costly **Pipeline A** steps: git scan (`git-commits-to-cv`) and Master rewrite (`summarize-into-doc` → **Master CV** / **Master CV EN**).
_Avoid_: Silent git history scans, silent Master overwrite/rewrite

### Planned Real Child Skills (canonical slugs)

**git-commits-to-cv**:
Existing **Real Child Skill** that extracts experience from git commits into Hybrid Artefacts in **Experience Memory**.
_Avoid_: Replacing it with a reference-only module

**optimize-linkedin-profile**:
Planned **Real Child Skill** for LinkedIn profile optimization. Canonical English slug. Reads **LinkedIn Profile Snapshot** (`output/linkedin/profile.md`) + **Goals Artefact** (**Hard Gate**); proposes improvements — does not auto-post to LinkedIn. Folder not created yet. Details: [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
_Avoid_: otimize-linkedin-profile, folding profile optimization into a reference-only module by default, auto-posting to LinkedIn, scraping LinkedIn as default intake

**adapt-cv-to-job**:
Planned **Real Child Skill** for job-specific CV adaptation. Reads the language-appropriate master (**Master CV** or **Master CV EN**) + **Experience Memory** + raw **Job Description** (recommended: **Career Inbox**); writes a **Tailored CV** at `output/cv/master_cv.<job-slug>.md` in the JD's language (**Hard Gate** on **Goals Artefact**). Does not overwrite either master. Canonical name in glossary; folder not created yet.
_Avoid_: Inventing alternate slugs without updating this glossary, shipping the skill folder before grilling finishes, writing under `output/cv/tailored/`, treating Portfolio CV as the adapt write target, requiring `master_cv.<job-slug>.en.md`

### Job plan

**Target Role**:
Primary job targets for applications and framing: Eng. Software Fullstack Pleno, Frontend Pleno, or closely related titles.
_Avoid_: Junior-only framing as default, unrelated roles without explicit override

**Location Preference**:
Preferred work arrangement: híbrido or remoto in São Paulo (SP), or fully remote (100% HO) abroad; abroad priority is LATAM.
_Avoid_: On-site-only SP as the only option, ignoring LATAM for exterior roles

**Comp Floor**:
Minimum acceptable compensation: greater than 10k BRL/mês (or equivalent when converted from another currency).
_Avoid_: Accepting below-floor offers as default plan, treating currency conversion as optional

**Company Shortlist**:
Curated target-company lists under **Career Output Root**: `output/companies/` — BR at `output/companies/br.md`, LATAM at `output/companies/latam.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\companies\`). Populated via **Agentic Career** / company-shortlist **Reference Module** steps — not invented ad hoc outside this tree.
_Avoid_: Scattering company lists outside `output/companies/`, inventing alternate filenames without updating this glossary, researching/filling real lists from stubs alone

**Company Entry**:
One row/block in a **Company Shortlist** file. Recommended default fields (user did **not** explicitly confirm tags — adopt as recommended default): name, link, tags for remote/hybrid, comp signal if known, stack, **Company Tier**.
_Avoid_: Omitting recommended fields without reason, inventing a rigid schema that blocks sparse entries, treating recommended defaults as user-locked requirements

**Company Tier**:
Priority band on a **Company Entry**: `dream` \| `realistic` \| `stretch`.
_Avoid_: Free-form tier labels without updating this glossary, omitting tier when ranking targets

**Study Plan**:
Single study-plan artefact under **Career Output Root**: `output/study/plan.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\study\plan.md`). Derived from **Goals Artefact** + recurring JD gaps / **Tailored CV** analyses. Written by the study-planning **Reference Module** (under `agentic-career/references/` — hybrid packaging; not a standalone skill).
_Avoid_: Multiple competing plan files as the default, inventing a standalone `study-planning` skill folder, filling real plan content from stubs alone

**Applications Log** (future optional):
Possible later tracker at `output/applications.md` under **Career Output Root**. Path reserved in layout docs; workflow and schema **unresolved / deferred** — not part of companies+study Decision A.
_Avoid_: Treating `applications.md` as locked or required now, inventing application-tracking workflow from this glossary alone

## Relationships

- **Agentic Career** owns **Career Output Root**; **Real Child Skills** and **Reference Modules** share that root
- **Skill Packaging (hybrid)** splits work: **Real Child Skills** are standalone; **Reference Modules** live under `agentic-career/references/`
- **Experience Memory** is a subtree of **Career Output Root**
- **Career Inbox** is a subtree of **Career Output Root**; raw only — not canonical experience
- **Goals Artefact** (`output/goals.md`) is user-instance data in **Career Output Root**; domain defaults for **Target Role**, **Location Preference**, and **Comp Floor** live in this glossary
- user-goals / goals-intake (**Reference Module**) reads/writes the **Goals Artefact**; re-runs use **Smart Merge**
- **Goals Intake Gating** (C): **Hard Gate** before `adapt-cv-to-job` and `optimize-linkedin-profile`; **Soft Gate** before **Consolidation** / `summarize-into-doc`, `git-commits-to-cv`, `append-data-to-cv`, `linkedin-post-ideas`, and study planning
- Soft-gated steps may proceed on glossary defaults when **Goals Artefact** is absent; hard-gated steps must not
- `git-commits-to-cv` writes Hybrid Artefacts into **Experience Memory** with **Artefact Source** `git`
- `append-data-to-cv` reads **Career Inbox**, normalizes into **Experience Memory** with **Artefact Source** `manual` \| `cv-import` \| `doc`
- **Consolidation** (`summarize-into-doc`) reads canonical **Experience Memory** (+ masters where relevant) — not raw **Career Inbox**
- `adapt-cv-to-job` reads language-appropriate master + **Experience Memory** + raw **Job Description** (recommended from **Career Inbox**); writes **Tailored CV** alongside masters — does not overwrite masters and does not treat inbox as Experience Memory
- **Consolidation** writes **Master CV** (PT) and may write **Master CV EN** under `output/cv/` — translating XYZ at Consolidation time without rewriting Hybrid Artefacts
- **Tailored CV** files share `output/cv/` via `master_cv.<job-slug>.md` (**Job Slug** = short kebab-case); content language follows the JD; may link to inbox JD and embed **JD Summary** for study-planning
- **CV Language Policy (dual-track)**: artefacts PT-BR only; dual masters; tailored = JD language; LinkedIn optimize = Snapshot primary language
- **Master CV** / **Master CV EN** and **Portfolio CV** are distinct; syncing masters → portfolio is optional **publish-cv**, not part of **Consolidation**
- **Target Role**, **Location Preference**, and **Comp Floor** constrain how career skills frame and filter opportunities
- **Company Shortlist** files live under `output/companies/` (`br.md`, `latam.md`); each **Company Entry** uses recommended fields including **Company Tier**
- **Study Plan** is a single file at `output/study/plan.md`; study-planning stays a **Reference Module** under `agentic-career/references/`
- Study-planning reads **Goals Artefact** + recurring JD gaps / **Tailored CV** (**JD Summary**) signals; writes **Study Plan**
- **Applications Log** (`output/applications.md`) is deferred — path optional/future only
- LinkedIn paste/export lands in **Career Inbox**; normalization produces **LinkedIn Profile Snapshot** at `output/linkedin/profile.md` (no CLI/scraper default) — see LinkedIn Resolved decision 2
- `optimize-linkedin-profile` reads **LinkedIn Profile Snapshot** + **Goals Artefact** (**Hard Gate**); proposes improvements; does not auto-post
- `linkedin-post-ideas` reads Snapshot + goals (**Soft Gate**) + **Master CV** / **Experience Memory**; writes **Post Ideas Artefact** at `output/linkedin/post-ideas.md`
- **Mother Routing**: CV-optimize intent → **CV Happy Path** / **Pipeline A**; otherwise → **Generic Invoke** / **Menu C**
- **Pipeline A** uses **Soft Gate** for goals on the CV path; runs append when inbox/materials exist; runs `git-commits-to-cv` only with user-provided repo paths; consolidates to dual masters; applies **Heavy-step Confirmation** before git scan and Master rewrite
- **Menu C** asks intent then dispatches module/skill (LinkedIn, study, companies, etc.)

## Example dialogue

> **Dev:** "Where should Hybrid Artefacts live now?"
> **Domain expert:** "Under **Experience Memory** inside **Career Output Root** — not under `portfolio/.specs`."
>
> **Dev:** "Is everything under `agentic-career` just references?"
> **Domain expert:** "No — that was an earlier B-only idea. **Skill Packaging (hybrid)**: `git-commits-to-cv`, `optimize-linkedin-profile`, and `adapt-cv-to-job` are **Real Child Skills**; intake, `append-data-to-cv`, `summarize-into-doc`, `linkedin-post-ideas`, and study planning stay as **Reference Modules**."
>
> **Dev:** "Does **Consolidation** update the portfolio `current_cv.md`?"
> **Domain expert:** "No. `summarize-into-doc` writes under `output/cv/`: **Master CV** at `master_cv.md` (PT) and may generate **Master CV EN** at `master_cv.en.md`. **Portfolio CV** sync is a separate explicit/manual **publish-cv** step — out of Consolidation scope for now."
>
> **Dev:** "Should Hybrid Artefacts or git-commits-to-cv become bilingual for the EN master?"
> **Domain expert:** "No. **CV Language Policy (dual-track)** = B: artefacts stay PT-BR only. Consolidation may translate XYZ into **Master CV EN** without rewriting artefacts. Each **Tailored CV** is one file; language follows the JD."
>
> **Dev:** "What roles are we optimizing for?"
> **Domain expert:** "**Target Role** defaults: Fullstack Pleno / Frontend Pleno (and close cousins), with **Location Preference** and **Comp Floor** as hard filters for the job plan."
>
> **Dev:** "Where do the user's live goals answers live?"
> **Domain expert:** "In the **Goals Artefact** at `output/goals.md` — instance data under **Career Output Root**, not in this glossary. Intake is the user-goals / goals-intake **Reference Module**; re-runs **Smart Merge**."
>
> **Dev:** "If `goals.md` is missing, can I still run Consolidation or adapt-cv-to-job?"
> **Domain expert:** "**Goals Intake Gating** is C: **Soft Gate** for Consolidation — warn, offer intake, then continue on glossary defaults if the user proceeds. **Hard Gate** for `adapt-cv-to-job` and `optimize-linkedin-profile` — must run intake / require `goals.md` first."
>
> **Dev:** "I pasted an old CV and a project write-up — where do they land, and what do Consolidation / adapt-cv-to-job read?"
> **Domain expert:** "Raw material goes to **Career Inbox** (`output/inbox/`). `append-data-to-cv` normalizes into Hybrid Artefacts under **Experience Memory** with **Artefact Source** `manual` / `cv-import` / `doc`. Consolidation reads `experience/` (+ **Master CV**), never raw inbox as experience. `adapt-cv-to-job` also reads Master + experience, plus raw **Job Description** from inbox (recommended). Inbox is gitignored for PII."
>
> **Dev:** "How do we get the LinkedIn profile in, and does optimize auto-post?"
> **Domain expert:** "Paste or export → **Career Inbox** → normalize to **LinkedIn Profile Snapshot** (`output/linkedin/profile.md`). No CLI/scraper default. `optimize-linkedin-profile` proposes only (**Hard Gate** on goals); `linkedin-post-ideas` writes `output/linkedin/post-ideas.md`."
>
> **Dev:** "Where does `adapt-cv-to-job` write the tailored CV, and where does the raw JD live?"
> **Domain expert:** "Output = B: **Master CV** stays at `output/cv/master_cv.md`; variants are `output/cv/master_cv.<job-slug>.md` beside it — no `tailored/` folder. Raw **Job Description** recommended default is **Career Inbox** (user didn't pick otherwise). The Tailored CV may link to that inbox file and embed a **JD Summary** so study-planning need not open the inbox."
>
> **Dev:** "Where do company shortlists and the study plan live?"
> **Domain expert:** "Decision A: **Company Shortlist** at `output/companies/br.md` and `output/companies/latam.md`; single **Study Plan** at `output/study/plan.md`. Study-planning stays a **Reference Module** under `agentic-career/references/`. **Company Entry** fields (name, link, remote/hybrid tags, comp signal, stack, tier) are recommended defaults — user didn't lock tags. `output/applications.md` is deferred."
>
> **Dev:** "User says 'otimizar currículo' — do we menu or run the CV pipeline?"
> **Domain expert:** "**CV Happy Path** → **Pipeline A**: soft-gate goals if missing, append if inbox/materials, `git-commits-to-cv` for missing repos (user gives each repo path — no filesystem auto-discovery), then Consolidation to `master_cv.md` + `master_cv.en.md`. Confirm before git scan and before rewriting Master."
>
> **Dev:** "User just says 'ajuda no LinkedIn' or asks about study/companies?"
> **Domain expert:** "**Generic Invoke** → **Menu C**: ask what to do, then dispatch the matching module/skill. Do not start **Pipeline A**."

## Flagged ambiguities

- ~~**Mother skill name**~~ — **resolved**: `agentic-career`.
- ~~**Docs layout**~~ — **resolved**: Option B — `CONTEXT-MAP.md` + separate contexts under `agentic-career/context/` (moved off repo root).
- ~~**Experience memory location**~~ — **resolved**: migrated from `portfolio/.specs/` to **Experience Memory** under **Career Output Root**; local duplicates under `portfolio/.specs/` **deleted** (Decision A) — sole canonical path, no dual copies / drift.
- ~~**Skill packaging**~~ — **resolved**: hybrid (not B-only references). See **Skill Packaging (hybrid)** and Resolved decision 8.
- ~~**Consolidation output path**~~ — **resolved**: Option B — **Master CV** under Career Output Root; **Portfolio CV** not auto-updated. See Resolved decision 9.
- ~~**User goals intake layout**~~ — **resolved**: Option A — single **Goals Artefact** (`output/goals.md`). See Resolved decision 10.
- ~~**Goals intake gating**~~ — **resolved**: Option C — **Hard Gate** vs **Soft Gate** by step. See Resolved decision 11.
- ~~**append-data-to-cv storage**~~ — **resolved**: Option B — **Career Inbox** + normalize into **Experience Memory**. See Resolved decision 12.
- ~~**LinkedIn profile intake**~~ — **resolved**: Option A — paste/export → **Career Inbox** → **LinkedIn Profile Snapshot**. See Resolved decision 13 and [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
- ~~**Company shortlists + study plan layout**~~ — **resolved**: Option A — `output/companies/br.md` + `latam.md`; single **Study Plan** at `output/study/plan.md`. See Resolved decision 15.
- ~~**Applications Log** (`output/applications.md`)~~ — **deferred to Phase 2** (path reserved; workflow not grilled). See Resolved decision 18.
- ~~**adapt-cv-to-job output layout**~~ — **resolved**: Option B — Tailored CVs alongside Master as `master_cv.<job-slug>.md`; raw JD → **Career Inbox** (recommended default). See Resolved decision 14.
- ~~**CV / LinkedIn language**~~ — **resolved**: Option B — dual-track. See Resolved decision 16 and **CV Language Policy (dual-track)**.
- ~~**Agentic Career routing**~~ — **resolved**: CV optimize intent → **Pipeline A**; generic invoke → **Menu C**. See Resolved decision 17.
- ~~**Design grill + Phase 1 scope**~~ — **resolved**: grill-with-docs closed (user choice **A**). Phase 1 ships CV pipeline Reference Modules + enriched mother skill; Phase 2 deferred. See Resolved decision 18.
- Behaviour/internals of planned **Real Child Skills** (`optimize-linkedin-profile` proposal-file layout; `adapt-cv-to-job` selection/rewrite algorithm) — unresolved / **Phase 2** (folders not created yet). Intake paths for LinkedIn and adapt-cv output paths are locked.
- ~~Full `append-data-to-cv` reference workflow~~ — **resolved for Phase 1**: normalize steps + inbox naming documented in `agentic-career/references/append-data-to-cv.md`. See Resolved decision 18.
- Who normalizes LinkedIn inbox → Snapshot (append-data vs dedicated step) — unresolved / **Phase 2**; paths locked.
- **publish-cv** internals (Master → Portfolio sync) — unresolved (future optional step).
- Study-planning / company-shortlist / `linkedin-post-ideas` **Reference Module** internals — unresolved / **Phase 2** (paths locked; content populated later).

## Resolved decisions

1. **Mother skill** = `agentic-career` — orchestrates CV + LinkedIn + study + jobs; entry for the full workflow; invokes or points to **Real Child Skills**.
2. **Docs layout** = Option B — `CONTEXT-MAP.md` + separate context files under `.agents/skills/portfolio/agentic-career/context/` (not one giant root `CONTEXT.md`; not at repo root). Root `CONTEXT.md` is only a repo pointer to skills/categories.
3. **Career Output Root** = `.agents/skills/portfolio/agentic-career/output/`; **Experience Memory** = `output/experience/` (artefacts migrated from `portfolio/.specs/`). Personal results under `output/` are gitignored except `**/README.md` placeholders.
4. **Target roles** = Eng. Software Fullstack Pleno / Frontend Pleno / correlatos.
5. **Location** = híbrido/remoto SP, or exterior 100% HO with LATAM priority abroad.
6. **Comp floor** = >10k BRL/mês (converted when needed).
7. **Portfolio `.specs` cleanup (Decision A)** = Hybrid Artefact `.md` files under `portfolio/.specs/` were deleted after migration; only `README.md` (migration pointer) remains. Sole canonical **Experience Memory** is `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\` — no local duplicates, no drift.
8. **Skill packaging (hybrid)** — supersedes prior "B — all under mother references only". **Real Child Skills** (standalone, invocável): `git-commits-to-cv` (exists), `optimize-linkedin-profile` (Phase 2; English slug, not otimize-…), `adapt-cv-to-job` (Phase 2). **Reference Modules** only (under `agentic-career/references/`, not standalone skills): user-goals / goals-intake (**Goals Artefact**), `append-data-to-cv`, `summarize-into-doc` (**Consolidation** → **Master CV** + **Master CV EN**; not summaryze), `linkedin-post-ideas` (Phase 2), study-planning (→ **Study Plan**, Phase 2), company-shortlist curation (Phase 2), other lightweight orchestration. Phase 1 ships the three CV pipeline reference modules + mother skill enrichment; planned child skill folders remain **not** created (Phase 2). See decision 18.
9. **Consolidation output = B** — `summarize-into-doc` writes **only** under Career Output Root `output/cv/`. Canonical working CV (PT) = **`master_cv.md`** (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.md`). English master = **`master_cv.en.md`** (see decision 16). Does **not** auto-update **Portfolio CV** at `c:\_git\projects\portfolio\public\assets\pdf\current_cv.md`. Sync to portfolio is a separate explicit/manual step (future optional **publish-cv**); out of Consolidation scope for now.
10. **User goals intake = A** — single **Goals Artefact** at `output/goals.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\goals.md`). Contents: target role(s), location prefs, comp floor, constraints, positioning hypotheses. Intake flow stays a **Reference Module** (user-goals / goals-intake under `agentic-career/references/`). Re-runs: **Smart Merge** (preserve confirmed user answers; merge new). Instance data in **Career Output Root** — not domain glossary in `career/CONTEXT.md`. File is created when intake runs (do not invent stub content beforehand).
11. **Goals Intake Gating = C** — mixed hard/soft by step. **Hard Gate** (must run goals intake / require `goals.md` before continuing): `adapt-cv-to-job`, `optimize-linkedin-profile`. **Soft Gate** (warn + offer intake; may continue with glossary defaults — Fullstack/Frontend Pleno, SP/híbrido-remoto/LATAM, >10k BRL): **Consolidation** / `summarize-into-doc`, `git-commits-to-cv`, `append-data-to-cv`, `linkedin-post-ideas`, study-planning modules. Resolves prior hard-vs-soft ambiguity.
12. **append-data-to-cv storage = B** — raw uploads/pastes land in **Career Inbox** at `output/inbox/` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\inbox\`). Normalization (Phase 1 Reference Module: `agentic-career/references/append-data-to-cv.md`) produces/updates Hybrid Artefacts under `output/experience/<company-slug>/` with metadata **Artefact Source** `manual` \| `cv-import` \| `doc` (aligned with Hybrid Artefact template; `git-commits-to-cv` uses `git`). **Consolidation** reads canonical **Experience Memory** (+ **Master CV**), not raw inbox. `adapt-cv-to-job` reads Experience Memory + Master CV for experience, and may also read raw **Job Description** from inbox (see decision 14) — inbox is never canonical experience. **All personal Career Output Root files are gitignored** — only `output/**/README.md` structure placeholders stay tracked (goals, experience artefacts, masters, LinkedIn snapshots, shortlists, study plan, inbox dumps).
13. **LinkedIn profile intake = A** — no official LinkedIn CLI / scraper as default. User paste or export → **Career Inbox** (`output/inbox/`) → normalize to **LinkedIn Profile Snapshot** at `output/linkedin/profile.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\profile.md`). `optimize-linkedin-profile` (planned Real Child Skill; folder not created yet) reads Snapshot + **Goals Artefact** (**Hard Gate**) and proposes improvements — does **not** auto-post to LinkedIn. `linkedin-post-ideas` (Reference Module) uses Snapshot + goals (**Soft Gate**) + Master CV / Experience Memory; preferred write path = `output/linkedin/post-ideas.md`. Domain detail: [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
14. **adapt-cv-to-job output = B** — **Master CV** stays at `output/cv/master_cv.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.md`). **Tailored CV** variants live **alongside** Master in the same folder: `output/cv/master_cv.<job-slug>.md` — **not** a `tailored/` subdirectory. **Job Slug** = short kebab-case from company+role or user-provided. Raw **Job Description**: recommended default = **Career Inbox** first (align with `append-data-to-cv`); user did **not** explicitly pick JD location — use this recommended default. Optional frontmatter/link in the Tailored CV pointing to the inbox JD file. Tailored CV may embed a **JD Summary** / requirements-extracted section so study-planning can work without opening inbox. Skill folder not created yet.
15. **Companies + study = A** — under **Career Output Root**: **Company Shortlist** BR = `output/companies/br.md`, LATAM = `output/companies/latam.md` (full dir: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\companies\`); single **Study Plan** = `output/study/plan.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\study\plan.md`), derived from goals + recurring JD gaps / Tailored CV analyses. Study-planning remains a **Reference Module** under `agentic-career/references/` (hybrid packaging — not a standalone skill). **Company Entry** recommended default fields (user did **not** explicitly confirm tags — adopt as recommended default): name, link, tags for remote/hybrid, comp signal if known, stack, **Company Tier** (`dream` \| `realistic` \| `stretch`). Do **not** research/fill real company lists or full study content from path stubs alone — populate later via agentic-career. Optional future **Applications Log** at `output/applications.md` — unresolved/deferred.
16. **CV / LinkedIn language = B (dual-track)** — Hybrid Artefacts and `git-commits-to-cv` remain **PT-BR only** (do not change cv-from-commits Resolved decision 7). **Master CV** PT = `output/cv/master_cv.md`. **Master CV EN** = `output/cv/master_cv.en.md`, generated at **Consolidation** / `summarize-into-doc` (may translate XYZ → EN master without rewriting artefacts). **Tailored CV**: one file per job at `master_cv.<job-slug>.md`; content language = JD language (EN job → EN content; filename stays without `.en` unless a later rule requires it). LinkedIn: `optimize-linkedin-profile` optimizes in the primary language of the existing **LinkedIn Profile Snapshot**; **Post Ideas Artefact** may be bilingual later. Do not invent `master_cv.en.md` content until Consolidation runs. LinkedIn detail: [linkedin/CONTEXT.md](../linkedin/CONTEXT.md).
17. **Agentic Career routing** — on mother invoke, route by intent:
    - **CV Happy Path** (intent: optimize CV / otimizar currículo) = **Pipeline A** with **Heavy-step Confirmation** before git scan and before rewriting Master: (1) goals intake if missing (**Soft Gate** for this path); (2) `append-data-to-cv` if **Career Inbox** has items / user has materials; (3) `git-commits-to-cv` for missing repos — **user provides Scanned repository path** (do not auto-discover filesystem); matches existing `git-commits-to-cv` skill inputs; adopted as resolved recommended default; (4) `summarize-into-doc` → **Master CV** (`master_cv.md`) + **Master CV EN** (`master_cv.en.md`).
    - **Generic Invoke** (e.g. “ajuda no LinkedIn”, study, companies) = **Menu C**: ask what to do, then dispatch the matching **Real Child Skill** / **Reference Module** (Phase 2 items = stubs until decision 18 Phase 2).
18. **Design grill closed + Phase 1 = A** — grill-with-docs design closed with user choice **A** (ship CV pipeline first; defer the rest).
    - **Phase 1 (implemented)**: enrich mother `agentic-career/SKILL.md`; ship **Reference Modules** under `agentic-career/references/` for the CV pipeline only — `goals-intake`, `append-data-to-cv`, `summarize-into-doc` — plus optional orchestration helper `cv-happy-path.md`. **Pipeline A** step 3 continues to invoke the existing sibling **Real Child Skill** at `.agents/skills/portfolio/git-commits-to-cv/` (user provides each Scanned repository path).
    - **Phase 2 (deferred)** — do **not** implement in Phase 1: Real Child Skill folders for `adapt-cv-to-job` and `optimize-linkedin-profile`; full `linkedin-post-ideas` Reference Module; study-planning / company-shortlist content filling (real companies); **Applications Log** (`applications.md`) workflow; LinkedIn inbox→Snapshot normalizer ownership. Menu C may list these as “Phase 2” stubs only.
    - Paths and glossary for deferred items remain locked from prior decisions; only internals/content are deferred.
