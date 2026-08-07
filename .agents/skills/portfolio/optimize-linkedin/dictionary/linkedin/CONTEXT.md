# LinkedIn

Domain context for **optimize-linkedin**: profile optimization and post ideas.

**Docs home**: `.agents/skills/portfolio/optimize-linkedin/dictionary/linkedin/` — not at the `agentic-ai` repo root.

Skill: `.agents/skills/portfolio/optimize-linkedin/` (sibling of `summarize-cv`; flat portfolio skills — no mother).

## Language

**Optimize LinkedIn Output Root**:
This skill's user data: `.agents/skills/portfolio/optimize-linkedin/output/`.
_Avoid_: Nesting LinkedIn artefacts under `summarize-cv/output/linkedin/`

**Summarize CV Output Root** (cross-read):
`.agents/skills/portfolio/summarize-cv/output/` — goals, masters, experience. LinkedIn skill may **read**; must not write CV/experience/goals here.
_Avoid_: Duplicating masters into LinkedIn output as source of truth

**Career Inbox** (shared raw landing — owned by summarize-cv):
`summarize-cv/output/inbox/` — preferred place for raw LinkedIn paste/export before normalization into Snapshot.
_Avoid_: Treating inbox paste as canonical profile

**LinkedIn Profile Snapshot**:
Normalized profile markdown: `optimize-linkedin/output/profile.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\optimize-linkedin\output\profile.md`).
_Avoid_: Scraping LinkedIn as default, inventing full profile before user material

**LinkedIn Intake**:
Paste/export → Career Inbox → normalize to **LinkedIn Profile Snapshot**.
_Avoid_: Official LinkedIn CLI / scrapers as default

**Profile optimization** / **optimize-linkedin** (profile mode):
Reads Snapshot + **Goals Artefact** (**Hard Gate**); proposes improvements in the Snapshot's primary language. Does not auto-post.
_Avoid_: Auto-posting, skipping Hard Gate, old folder name nesting under summarize-cv

**Post Ideas Artefact**:
`optimize-linkedin/output/post-ideas.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\optimize-linkedin\output\post-ideas.md`).
_Avoid_: Auto-publishing ideas to LinkedIn

**post-ideas mode**:
Drafts post ideas from Snapshot + goals (**Soft Gate**) + Master CV / Experience Memory (cross-read). Writes **Post Ideas Artefact**.
_Avoid_: Creating a separate `linkedin-post-ideas` skill folder

## Relationships

- LinkedIn owns its output root; cross-reads summarize-cv for goals/masters/experience
- Intake raw → summarize-cv inbox → Snapshot under optimize-linkedin/output
- Skill is currently a **deferred stub** — paths locked; internals TBD
- Language aligns with CV dual-track: optimize in Snapshot primary language; post-ideas bilingual later optional

## Example dialogue

> **Dev:** "Should we scrape LinkedIn?"
> **Domain expert:** "No. Paste/export → Career Inbox → Snapshot at `optimize-linkedin/output/profile.md`."
>
> **Dev:** "Does optimize auto-post?"
> **Domain expert:** "No. Proposals only (**Hard Gate** on goals)."

## Flagged ambiguities

- Proposal-file layout for profile mode — unresolved
- Snapshot schema — unresolved
- Who normalizes inbox → Snapshot — unresolved; paths locked
- Skill implementation beyond stub — deferred

## Resolved decisions

1. LinkedIn is a **sibling skill** (`optimize-linkedin`), not a subtree of summarize-cv output.
2. Intake = paste/export → Career Inbox → Snapshot at `optimize-linkedin/output/profile.md`.
3. Profile mode: Snapshot + Goals (**Hard Gate**); no auto-post.
4. Post-ideas mode: Snapshot + goals (**Soft Gate**) + Master/experience; write `output/post-ideas.md`.
5. Language: Snapshot primary language for optimize; post-ideas bilingual later optional.
6. Redesign grill 2026-08-06 — moved out of former `agentic-career`; post-ideas is an internal mode, not a separate skill.
