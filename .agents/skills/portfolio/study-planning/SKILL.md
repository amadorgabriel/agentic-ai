---
name: study-planning
description: >-
  Plan deliberate study and maintain BR/LATAM company shortlists from career
  goals and recurring JD gaps. Stub — full workflow deferred. Use when the user
  explicitly invokes study-planning, asks for a study plan, or company shortlists.
disable-model-invocation: true
---

# Study Planning

**Status: deferred stub.** Do not invent a full study plan or research real company lists from stubs alone.

Categoria: **portfolio**.

## Output (this skill)

```
c:\_git\projects\agentic-ai\.agents\skills\portfolio\study-planning\output\
```

| Path | Role |
| --- | --- |
| `companies/br.md` | Company Shortlist — BR |
| `companies/latam.md` | Company Shortlist — LATAM |
| `study/plan.md` | Study Plan |

## Cross-reads (allowed)

May **read** Summarize CV Output Root:

- `../summarize-cv/output/goals.md`
- `../summarize-cv/output/cv/master_cv*.md` (including Tailored CVs / JD Summary)
- `../summarize-cv/output/experience/`

## Current behaviour

1. Explain that planning content is deferred.
2. Show existing stub files under `output/` if useful.
3. For CV/experience work → suggest `summarize-cv`.
4. Do **not** fill real shortlists or a full study curriculum unless the user explicitly starts a future implementation session.
