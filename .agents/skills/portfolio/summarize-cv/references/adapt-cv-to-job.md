# Adapt CV to Job

**Reference Module** under `summarize-cv`. Produz um **Tailored CV** a partir do master + Experience Memory + JD.

Fonte: [dictionary/cv/CONTEXT.md](../dictionary/cv/CONTEXT.md) (Resolved 14, 19).

## Paths

| Artefact | Path |
| --- | --- |
| Master CV (PT) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\cv\master_cv.md` |
| Master CV EN | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\cv\master_cv.en.md` |
| Tailored CV | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\cv\master_cv.<job-slug>.md` |
| Experience Memory | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\experience\**\*.md` |
| Goals | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\goals.md` |
| Career Inbox (JD) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\summarize-cv\output\inbox\` |

## Preconditions

1. **Hard Gate** — `output/goals.md` must exist. If missing: run [goals-intake.md](./goals-intake.md) or refuse to continue.
2. At least one master should exist (`master_cv.md` and/or `master_cv.en.md`). If neither exists: offer Pipeline A Consolidation first; do not invent a master from scratch here unless user explicitly insists on a one-shot adapt from experience only (then warn quality risk).
3. Raw **Job Description** available — paste/upload into **Career Inbox** (recommended filename: `jd_<job-slug>.md` or `YYYY-MM-DD_jd_<job-slug>.md`).

## Inputs to collect

| Input | Required | Notes |
| --- | --- | --- |
| Job Description | Yes | Path under inbox, or paste then save to inbox before writing Tailored CV |
| `job-slug` | Yes | Short kebab-case (company + role hint) |
| Target language | Auto | Follow JD language (PT → base on Master PT; EN → base on Master EN if present, else translate from PT master) |
| Emphasis notes | No | User hints (must-have skills, omit companies, length) |

## Workflow

1. **Load goals** — confirm Target Role / constraints still apply; note positioning.
2. **Parse JD** — extract: title, must-have skills, nice-to-haves, seniority signals, domain keywords, language.
3. **Choose base master** — PT JD → `master_cv.md`; EN JD → prefer `master_cv.en.md`, else translate/adapt from PT.
4. **Select evidence** — from Experience Memory XYZ bullets (and masters), prioritize bullets that match must-haves; keep honesty (no invented metrics; keep `[MÉTRICA A CONFIRMAR]` if present).
5. **Rewrite** — produce one Tailored CV:
   - Optional YAML/frontmatter: `job_slug`, `jd_inbox_path`, `generated_at`, `based_on` (master file)
   - Section **JD Summary** (short: role, must-haves, keywords) for later `study-planning`
   - Summary/profile line aligned to JD + goals positioning
   - Experience bullets reordered/trimmed for relevance (still XYZ; PT-BR artefacts stay PT in memory — only the Tailored file follows JD language)
   - Skills/stack section reflecting JD overlap without fake proficiency
6. **Write** `output/cv/master_cv.<job-slug>.md` — **never** overwrite `master_cv.md` / `master_cv.en.md`.
7. **Confirm with user** — show slug path + what was emphasized/dropped; offer one revision pass.

## Tailored CV skeleton

```markdown
---
job_slug: <job-slug>
jd_inbox_path: inbox/<file>.md
based_on: cv/master_cv.md   # or master_cv.en.md
generated_at: <ISO-8601>
---

# <Name> — <Target title from JD/goals>

## JD Summary

- Role: …
- Must-haves: …
- Keywords: …

## Perfil

…

## Experiência

…

## Skills

…
```

(Adjust section names to match the base master's structure; keep ATS-friendly plain markdown.)

## Hard rules

| Do | Don't |
| --- | --- |
| Hard Gate on goals | Proceed without `goals.md` |
| Land/persist JD in inbox | Rely only on chat without saving JD |
| Write `master_cv.<job-slug>.md` | Overwrite masters or use `cv/tailored/` |
| Embed JD Summary | Dump full raw JD into Experience Memory |
| Match JD language | Invent bilingual dual tailored files |
| Prefer real XYZ evidence | Invent metrics or roles |

## After adapt

- Gaps vs JD may inform sibling **`study-planning`** (user invokes separately).
- Do not auto-run study or LinkedIn from this module.
