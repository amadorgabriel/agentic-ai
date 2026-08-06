# Career Inbox

Landing zone for **raw** career inputs before normalization into Hybrid Artefacts.

Path: `.agents/skills/portfolio/agentic-career/output/inbox/`

## Purpose

- Drop uploads, pastes, exports, and other unstructured material here (CVs, notes, docs, screenshots text, LinkedIn paste/export, raw **Job Description**s, etc.).
- The `append-data-to-cv` Reference Module (when implemented) reads from this inbox, then **normalizes** into Hybrid Artefacts under `../experience/<company-slug>/`.
- LinkedIn paste/export also lands here, then normalizes to **LinkedIn Profile Snapshot** at `../linkedin/profile.md` (no CLI/scraper default). See [../linkedin/README.md](../linkedin/README.md).
- Raw JDs for `adapt-cv-to-job`: **recommended default** landing zone (align with append-data; user did not pick otherwise). See Career Resolved decision 14 and [../cv/README.md](../cv/README.md).
- **Consolidation** reads canonical **`experience/`** (+ Master CV) — **not** this inbox as experience. `adapt-cv-to-job` reads experience + Master from canonical paths, and may read raw JD from here.

## Rules

- Treat contents as potentially sensitive (**PII**). Inbox files are **gitignored by default** (except this README).
- Do not treat inbox files as Experience Memory.
- Do not invent a full append/normalize workflow from this README alone — still grilling / not implemented yet.

## Related

- Career context: [context/career/CONTEXT.md](../../context/career/CONTEXT.md) (Resolved decision 12 — storage = B)
- Experience Memory: `../experience/`
- Master CV: `../cv/master_cv.md`
