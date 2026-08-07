---
name: optimize-linkedin
description: >-
  Optimize LinkedIn profile and/or draft post ideas using a profile snapshot and
  career goals. Stub — full workflow deferred. Use when the user explicitly
  invokes optimize-linkedin, asks to otimizar perfil LinkedIn, or wants LinkedIn
  post ideas.
disable-model-invocation: true
---

# Optimize LinkedIn

**Status: deferred stub.** Do not invent full profile content or auto-post to LinkedIn.

Categoria: **portfolio**. Dictionary: [dictionary/linkedin/CONTEXT.md](dictionary/linkedin/CONTEXT.md).

## Modes (when implemented)

| Mode | Behaviour |
| --- | --- |
| **profile** | Normalize intake → **LinkedIn Profile Snapshot**; propose optimizations (**Hard Gate** on goals) |
| **post-ideas** | Draft **Post Ideas Artefact** (**Soft Gate** on goals) |

## Paths (this skill)

```
c:\_git\projects\agentic-ai\.agents\skills\portfolio\optimize-linkedin\output\
```

| File | Role |
| --- | --- |
| `profile.md` | LinkedIn Profile Snapshot (reserved) |
| `post-ideas.md` | Post Ideas Artefact (reserved) |

## Cross-reads (allowed)

May **read** (not write) Summarize CV Output Root:

- `../summarize-cv/output/goals.md`
- `../summarize-cv/output/cv/master_cv.md` (+ EN)
- `../summarize-cv/output/experience/`

Raw LinkedIn paste/export: prefer landing in `../summarize-cv/output/inbox/` then normalize into `output/profile.md` here (see dictionary).

## Current behaviour

1. Explain that the skill is a stub.
2. Point at dictionary paths and reserved output files.
3. If user only needs CV work → suggest invoking `summarize-cv`.
4. Do **not** write fake `profile.md` / `post-ideas.md` unless the user provides real material **and** explicitly asks to persist a draft snapshot.
