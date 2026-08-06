---
name: git-commits-to-cv
description: >-
  Gera bullets de experiência de CV (XYZ + STAR) a partir do histórico de commits
  de um repositório git e grava um Memory artefact em Experience Memory (Agentic
  Career). Use when the user asks to gerar bullets de experiência do CV a partir
  de commits, commits → experiência, STAR/XYZ do repo X, extrair conquistas do
  git para o currículo, or explicitly invokes git-commits-to-cv.
disable-model-invocation: true
---

# Git Commits → CV Experience

Turn one **Scanned repository** into a **Hybrid Artefact** (XYZ bullets + STAR notes) under **Experience Memory**. Does **not** write `current_cv.md`.

Domain source of truth: [agentic-career/context/cv-from-commits/CONTEXT.md](../agentic-career/context/cv-from-commits/CONTEXT.md) (see also [CONTEXT-MAP.md](../agentic-career/context/CONTEXT-MAP.md)). Do not invent decisions beyond it.

Child capability of **Agentic Career** (`agentic-career`). Categoria: **career** — ver [README da categoria](../README.md).

## When to run

Only on **explicit** user request (this skill has `disable-model-invocation: true`). Do not auto-run during casual CV/portfolio talk.

## Quick checklist

```
Skill run progress:
- [ ] 1. Collect inputs
- [ ] 2. Resolve author allowlist (+ discovery)
- [ ] 3. Gather & theme commits (Commit Window)
- [ ] 4. Write 5–8 XYZ + STAR (PT-BR; no invented metrics)
- [ ] 5. Write or Smart Merge artefact
- [ ] 6. Present validation checklist + ask Y only for top bullets
```

## Step 1 — Inputs (ask if missing)

| Input | Required | Notes |
| --- | --- | --- |
| Scanned repository path | Yes | Absolute path to one git repo |
| `company-slug` | Yes | Path segment under Experience Memory |
| `project-slug` | Yes | Artefact filename (sans `.md`) |
| Commit Window | Yes* | Employment period for that project/company, **or** `--since` / date range if user provides it |
| Target Role Bias | No | Default: **Fullstack Engineer Pleno**. Allowed: `neutral`, `Frontend Pleno` |
| Author allowlist override | No | Include/exclude emails for this run |

\* If employment dates and `--since` are both missing, ask before scanning unbounded history.

**Output path** (create dirs as needed):

```
c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\<company-slug>\<project-slug>.md
```

Never write into the scanned repo. Never write `current_cv.md`. Do not write to `portfolio/.specs/` (migrated).

## Step 2 — Author filter

**Default allowlist:**

- `gabrielramador2014@gmail.com`
- `gabriel.amador@spott.eco`
- `amadorgabriel.dev@gmail.com`
- `gabriel.amador@etiquetacerta.com`

**Discover** distinct author emails in the scanned repo, then ask about any **not** already on the allowlist (or prior-run config) before gathering commits. Per-run include/exclude is allowed.

```bash
# From scanned repo root — portable
git shortlog -se --all
git log --all --format='%ae' | sort -u
```

PowerShell note: `sort -u` may need `Sort-Object -Unique` if `sort` is not GNU. Prefer the `git shortlog` / `git log --format` forms above.

Stop and ask if newly discovered emails appear. Do not silently include them.

## Step 3 — Gather commits

Filter by final allowlist **and** Commit Window. Group into themes/achievements — **not** one bullet per commit.

Prefer meaningful clusters: features, migrations, perf, infra, APIs, auth, data, FE ownership (aligned with Target Role Bias without inventing work).

```bash
# Example: allowlist + since (repeat --author as needed)
git log --since='2024-01-01' --until='2025-12-31' \
  --author='gabrielramador2014@gmail.com' \
  --author='gabriel.amador@spott.eco' \
  --author='amadorgabriel.dev@gmail.com' \
  --author='gabriel.amador@etiquetacerta.com' \
  --pretty=format:'%h|%ad|%ae|%s' --date=short

# Optional: denser signal for a theme
git log --since='2024-01-01' --author='amadorgabriel.dev@gmail.com' --oneline --grep='auth'
```

Detailed clustering heuristics → [references/workflow.md](references/workflow.md).

## Step 4 — Write bullets

- **Language**: PT-BR only
- **Count**: **5–8 XYZ Bullets** (top achievements)
- **Hybrid**: XYZ for CV + STAR Notes per achievement for interviews
- **Target Role Bias**: default Fullstack Pleno — prioritize API/data/auth/cloud/FE evidence **present in commits**; never invent work
- **Metrics**: NEVER invent. Use `[MÉTRICA A CONFIRMAR]` when Y lacks evidence. Put every placeholder on the **Validation Checklist**. Ask interactively **only** for top bullets missing Y.

Methods and examples → [references/methods.md](references/methods.md).

## Step 5 — Output / re-run

1. If artefact **does not exist**: write full Hybrid Artefact from [references/artefact-template.md](references/artefact-template.md).
2. If artefact **exists**: **Smart Merge**
   - Update bullets from new commit evidence
   - Preserve user-confirmed metrics and existing STAR Notes
   - Ask only when merge is ambiguous (conflicting claim, unclear whether to replace a bullet, etc.)

Do **not** perform Consolidation into `current_cv.md`.

## Artefact must include

- Metadata: repo path, Commit Window, emails used, generated-at, Target Role Bias
- Section: XYZ Bullets (5–8)
- Section: STAR Notes (per achievement)
- Section: Validation Checklist
- Optional: commit evidence refs (hashes / themes)

Template → [references/artefact-template.md](references/artefact-template.md).

## Hard rules

| Do | Don't |
| --- | --- |
| One scanned repo per run | Multi-repo aggregate |
| Write under Experience Memory | Write into scanned repo, `portfolio/.specs`, or `current_cv.md` |
| PT-BR Hybrid Artefact | EN sections / bilingual v1 |
| Ask on discovered emails | Auto-include unknown authors |
| `[MÉTRICA A CONFIRMAR]` | Invent numbers |
| Smart Merge on re-run | Blind overwrite of confirmed metrics/STAR |
| Explicit invocation only | Auto-run on casual CV chat |

## References

- [references/workflow.md](references/workflow.md) — detailed gather/theme/merge steps
- [references/methods.md](references/methods.md) — XYZ + STAR (PT-BR, ATS)
- [references/artefact-template.md](references/artefact-template.md) — output skeleton
