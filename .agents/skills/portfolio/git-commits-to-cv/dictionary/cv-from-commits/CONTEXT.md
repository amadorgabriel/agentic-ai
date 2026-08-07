# CV Experience from Commits

Domain context for a skill that turns git commit history into durable, per-project experience memory for a CV — without writing the final CV itself.

Skill: `.agents/skills/portfolio/git-commits-to-cv/` (sibling of **summarize-cv**)

**Hosting note**: this domain context lives at `.agents/skills/portfolio/git-commits-to-cv/dictionary/cv-from-commits/CONTEXT.md`. **Experience Memory** is under the **Summarize CV Output Root** (`summarize-cv/output/experience/`). Scanned repositories remain git-history input only.

## Language

**Skill run**:
One execution of the skill against a single git repository.
_Avoid_: Batch run, multi-repo scan, aggregated pass

**Scanned repository**:
The one git repository in scope for a **Skill run** — git history input only. Artefacts are never written here by default.
_Avoid_: Workspace, monorepo aggregate, multi-root folder, Experience Memory, Summarize CV Output Root

**Experience Memory**:
Directory under the **Summarize CV Output Root** where **Memory artefacts** are written: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\experience\`.
_Avoid_: Portfolio Memory Root, `portfolio/.specs`, scanned repository root, nested `.specs/` inside the scanned repo

**Company slug**:
Stable identifier for the employer or client in the memory path.
_Avoid_: Company name (raw), org display title

**Project slug**:
Stable identifier for the product or engagement within a company.
_Avoid_: Repo name (unless identical by convention), folder name

**Memory artefact**:
Durable markdown at `<Experience Memory>/<company-slug>/<project-slug>.md` holding CV-ready experience bullets derived from commits for one project.
_Avoid_: CV file, résumé draft, Master CV, Portfolio CV, scratch notes

**Experience bullet**:
A single CV-oriented statement of impact derived from commit evidence in the **Scanned repository**. Final CV-ready form is an **XYZ Bullet**.
_Avoid_: Commit message dump, changelog entry, raw diff summary, long STAR prose

**XYZ Bullet**:
CV-ready impact line in Google XYZ form: “Accomplished X as measured by Y by doing Z”. This is what **Consolidation** pulls into the **Master CV**.
_Avoid_: STAR prose, multi-paragraph achievement write-up

**STAR Note**:
Optional interview-prep block (Situation, Task, Action, Result) paired with an achievement inside a **Hybrid Artefact**. Not consolidated into the CV by default.
_Avoid_: CV bullet, XYZ line, default content of the **Master CV**

**Hybrid Artefact**:
A **Memory artefact** that stores **XYZ Bullets** as the CV-ready layer and optional **STAR Notes** per achievement for interview prep. Metadata includes **source** provenance (`git` for this skill; `manual` \| `cv-import` \| `doc` when produced by `append-data-to-cv` normalization — see Career context).
_Avoid_: STAR-only memory, XYZ-only memory (without optional STAR), dumping STAR into the **Master CV**, omitting `source` on new artefacts

**Artefact Source**:
Metadata field `source` on a **Hybrid Artefact**. This skill sets `git`. Other values (`manual`, `cv-import`, `doc`) come from Career inbox normalization — not from commit extraction.
_Avoid_: Using `manual`/`cv-import`/`doc` for commit-derived artefacts, inventing alternate labels without updating glossaries

**Consolidation**:
Later **Reference Module** step (`summarize-into-doc`, owned at Career context) that merges **XYZ Bullets** from **Experience Memory** into the **Master CV** (`output/cv/master_cv.md`) and may generate **Master CV EN** (`output/cv/master_cv.en.md`) by translating those PT-BR XYZ lines — without rewriting Hybrid Artefacts. Does not write the **Portfolio CV**. This skill does not perform Consolidation.
_Avoid_: Inline CV write by this skill, auto-updating portfolio `current_cv.md`, STAR-into-CV by default, rewriting artefacts to English for the EN master

**Master CV**:
Canonical working CV in PT-BR under Summarize CV Output Root (`output/cv/master_cv.md`). Consolidation write target — not written by this skill. English pair is **Master CV EN** (`master_cv.en.md`) at Career context — also not written by this skill.
_Avoid_: Portfolio `current_cv.md` as the working draft, expecting this skill to emit EN masters or bilingual artefacts

**Portfolio CV**:
Published portfolio site CV (`portfolio/public/assets/pdf/current_cv.md`). Not a Consolidation write target. Full definition in Career context.
_Avoid_: Conflating with **Master CV**, expecting this skill or Consolidation to update it

**Author Email Allowlist**:
Emails treated as "self" when filtering commits for a **Skill run**. Starts from known defaults; may gain per-run includes or excludes after user confirmation of **Discovered Collaborator Emails**.
_Avoid_: All commit authors, org-wide collaborator list, unverified discovered emails

**Discovered Collaborator Email**:
An email that appears as commit author/collaborator in the **Scanned repository** (e.g. via `git log --format` / shortlog) and is not already in the default allowlist or prior-run config. Presented to the user for include/exclude before filtering.
_Avoid_: Default allowlist email, automatic include without confirmation

**Metric Placeholder**:
Literal marker `[MÉTRICA A CONFIRMAR]` used in an **XYZ Bullet** when the Y (measure) lacks evidence in git/PRs/docs. Never invent a number to fill Y.
_Avoid_: Fabricated metric, guessed percentage, invented latency/throughput figure

**Validation Checklist**:
Artefact section listing items the user must confirm before treating metrics (or other unverified claims) as final — especially any **Metric Placeholder** and interactively proposed numbers.
_Avoid_: Silent assumption that placeholders are true, auto-resolving metrics without user confirmation

**Target Role Bias**:
Configurable framing mode for a **Skill run** that steers how commit evidence is prioritized and phrased in **Experience bullets**. Default: Fullstack Engineer Pleno (~5 years experience). Other allowed modes: neutral, Frontend Pleno. Never invent work absent from git history.
_Avoid_: Invented full-stack ownership, fabricating API/data/auth/cloud/FE work not in commits, hard-coded single role with no per-run override

**Smart Merge**:
Re-run policy for an existing **Memory artefact**: update bullets from new commit evidence; preserve user-confirmed metrics and **STAR Notes**; ask the user only when the merge is ambiguous.
_Avoid_: Blind overwrite, discard confirmed metrics, silent conflict resolution, ask-on-every-bullet

**Commit Window**:
Date range used to filter commits in a **Skill run**. Default: employment period for that project/company. Override: `--since` / explicit date range when the user provides it.
_Avoid_: Entire repo history by default, unbounded scan without employment or date bounds

## Relationships

- A **Skill run** targets exactly one **Scanned repository**
- A **Memory artefact** is written under **Experience Memory**, not into the **Scanned repository**
- A **Memory artefact** belongs to one **Company slug** + **Project slug** pair
- A **Skill run** updates at most one **Memory artefact** for the project under scan
- On re-run, a **Skill run** applies **Smart Merge** to the existing **Memory artefact**
- Hybrid Artefacts written by this skill set **Artefact Source** `git` (distinct from Career Inbox / append-data paths)
- **Consolidation** reads **XYZ Bullets** from many **Memory artefacts** into the **Master CV** (and may translate them into **Master CV EN**); this skill does not perform **Consolidation** and does not write CV files or the **Portfolio CV**
- **Experience bullets** (**XYZ Bullets**) live inside a **Hybrid Artefact**, not in the **Master CV** — always PT-BR; EN translation happens only at Consolidation if needed
- Optional **STAR Notes** live in the same **Hybrid Artefact** for interview prep; they are not consolidated into the **Master CV** by default
- `agentic-ai` hosts the skill and **Experience Memory** (under **Summarize CV Output Root**); scanned repos are git-history input only
- A **Skill run** filters commits by **Author Email Allowlist** and **Commit Window**

## Example dialogue

> **Dev:** "Can one **Skill run** scan my whole workspace and fill every project's **Memory artefact**?"
> **Domain expert:** "No — one **Scanned repository** per **Skill run**. Mixing repos mixes contexts."
>
> **Dev:** "So this skill should rewrite the **Master CV** or portfolio `current_cv.md` when it's done?"
> **Domain expert:** "No. It only maintains the **Memory artefact** in PT-BR. **Consolidation** later reads those **XYZ Bullets** into the **Master CV** (and may generate **Master CV EN** by translating XYZ — without rewriting artefacts) — and still does not write the **Portfolio CV**."
>
> **Dev:** "Why not one big artefact per company?"
> **Domain expert:** "Per-project memory stays ATS-friendly per company and keeps commit-derived bullets scoped to the right engagement."
>
> **Dev:** "Should memory live next to the scanned repo's commits?"
> **Domain expert:** "No. Write under **Experience Memory** in the **Summarize CV Output Root** so CV siblings share one experience store."
>
> **Dev:** "If I re-run and the artefact already has confirmed metrics, what happens?"
> **Domain expert:** "**Smart Merge** — update from new evidence, keep confirmed metrics and STAR, ask only when ambiguous."

## Flagged ambiguities

- ~~**`.specs/` / memory root location**~~ - **resolved** (see Resolved decisions #5 and #14): migrated then local duplicates deleted (Decision A).
- ~~**Bullet framing**~~ — **resolved** (see Resolved decisions #6): Hybrid (**XYZ Bullets** + optional **STAR Notes**).
- ~~**Language**~~ — **resolved** (see Resolved decisions #7): PT-BR only for artefacts. Career dual-track (masters EN/PT) does **not** change this skill — Consolidation may translate XYZ → EN master without rewriting artefacts (Career decision 16).
- ~~**Author identity filter**~~ — **resolved** (see Resolved decisions #8): hybrid allowlist + per-run discovery.
- ~~**Metric honesty rules**~~ — **resolved** (see Resolved decisions #9): never invent metrics; **Metric Placeholder** + **Validation Checklist**; ask only for top/high-value bullets.
- ~~**Target role bias**~~ — **resolved** (see Resolved decisions #10): configurable per run; default Fullstack Engineer Pleno.
- ~~**Skill auto-invocation policy**~~ — **resolved** (see Resolved decisions #11): explicit invocation only; do not auto-run on casual CV/portfolio talk.
- ~~**Bullet count / date range**~~ — **resolved** (see Resolved decisions #12): default **5–8 XYZ Bullets**; **Commit Window** = employment period or user-provided `--since` / date range.
- ~~**Re-run merge policy**~~ — **resolved** (see Resolved decisions #13): **Smart Merge**.
- ~~**Consolidation path**~~ — **resolved** at Career context (decision 9): **Master CV** under Summarize CV Output Root; this skill still never writes CV files.
- ~~**Artefact Source for this skill**~~ — **resolved** (see Resolved decisions #15): `source: git`; Career Inbox / append-data uses other values.

## Resolved decisions

1. **Execution scope**: one git repository per **Skill run**; do not aggregate multiple repos.
2. **Memory artefact path pattern**: `experience/<company-slug>/<project-slug>.md` under **Summarize CV Output Root** — one artefact per project.
3. **Consolidation boundary**: this skill does not write the **Master CV** or **Portfolio CV**; **Consolidation** (`summarize-into-doc`) is a later Career Reference Module that reads **XYZ Bullets** → **Master CV** only.
4. **Rationale**: avoid mixed contexts; ATS-friendly per company; stronger per-project memory.
5. **Memory artefact root**: **Experience Memory** at `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\experience\`. Full path pattern: `…\experience\<company-slug>\<project-slug>.md`. Scanned repos are git-history input; they are not the write target. (Supersedes the former **Portfolio Memory Root** at `portfolio/.specs/`.)
6. **Bullet format = Hybrid**: Final CV-ready bullets are **XYZ Bullets** (Google XYZ: “Accomplished X as measured by Y by doing Z”). The same **Hybrid Artefact** may also include optional **STAR Notes** (Situation, Task, Action, Result) per achievement for interview prep. Do not put long STAR prose into the **Master CV** by default — only **XYZ Bullets** consolidate into the **Master CV**.
7. **Artefact language = PT-BR only**: **Memory artefacts** (XYZ Bullets and STAR Notes) are written in Brazilian Portuguese. No bilingual sections; no EN flag in v1 of the skill. Unchanged by Career **CV Language Policy (dual-track)** (Career Resolved decision 16): **Master CV EN** is produced at Consolidation by translating XYZ — this skill never rewrites artefacts into English.
8. **Author identity filter = hybrid**: Commits count as "self" only if the author email is on the **Author Email Allowlist**. Defaults: `gabrielramador2014@gmail.com`, `gabriel.amador@spott.eco`, `amadorgabriel.dev@gmail.com`, `gabriel.amador@etiquetacerta.com`. Each **Skill run** discovers emails that appear as commit authors/collaborators in the **Scanned repository** (e.g. `git log --format` / shortlog). Newly discovered emails (not in defaults / prior-run config) are **Discovered Collaborator Emails** — present them and **ask the user** whether to include for this run. Per-run override/exclude is allowed.
9. **Metric honesty**: NEVER invent metrics. When Y (measure) in an **XYZ Bullet** lacks evidence in git/PRs/docs, use the **Metric Placeholder** `[MÉTRICA A CONFIRMAR]`. Each **Memory artefact** includes a **Validation Checklist** of items the user must confirm. For top/high-value bullets only: if a strong achievement lacks a number, ask the user interactively during the run. Weaker bullets: omit fabricated Y or use the placeholder without interrupting.
10. **Target Role Bias**: Configurable per **Skill run**. Default: Fullstack Engineer Pleno (~5 years experience) — when summarizing commits, prioritize and phrase evidence that supports full-stack ownership (API, data, auth, cloud, FE) without inventing work that is not in the git history. Other allowed modes: neutral, Frontend Pleno.
11. **Skill invocation = explicit only**: The skill must set `disable-model-invocation: true`. It runs only when the user explicitly asks — e.g. generate CV experience from a repo, commits → experience bullets, or STAR/XYZ from project X. Do **not** auto-run when the user is casually discussing CV/portfolio.
12. **Default output count + Commit Window**: Produce **5–8 XYZ Bullets** (top achievements, not one-per-commit). **Commit Window** defaults to the employment period for that project/company; if the user provides `--since` or an explicit date range, use that instead.
13. **Re-run = Smart Merge**: If the **Memory artefact** already exists, **Smart Merge** — update bullets from new evidence; preserve user-confirmed metrics and **STAR Notes**; ask the user only when the merge is ambiguous.
14. **Migration from portfolio/.specs (Decision A)**: Existing Hybrid Artefacts were migrated from `C:\_git\projects\portfolio\.specs\` into **Experience Memory**, preserving company/project relative paths. Local Hybrid Artefact `.md` duplicates under `portfolio/.specs/` were then **deleted by design** (only `README.md` migration pointer remains) so the sole canonical store is **Experience Memory** — no dual copies / drift. New runs must write only to **Experience Memory**.
15. **Artefact Source on commit-derived artefacts** = `git`. Aligns with Career Resolved decision 12 (`append-data-to-cv` storage = B): Hybrid Artefact template metadata field `source` is `git` \| `manual` \| `cv-import` \| `doc`. This skill only writes `git`; it does not use **Career Inbox**.
