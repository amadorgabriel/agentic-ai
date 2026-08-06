# LinkedIn

Domain context for LinkedIn profile optimization and post ideas under **Agentic Career**. Shared user data uses the same **Career Output Root** as other career skills. Intake is paste/export via **Career Inbox** — no LinkedIn CLI or scraper as default.

**Docs home**: `.agents/skills/portfolio/agentic-career/context/linkedin/` (see [CONTEXT-MAP.md](../CONTEXT-MAP.md)). Not at the `agentic-ai` repo root.

## Language

**Career Output Root**:
Shared memory for career skills: `.agents/skills/portfolio/agentic-career/output/` (see [career/CONTEXT.md](../career/CONTEXT.md)).
_Avoid_: Separate LinkedIn-only data root without shared career memory

**LinkedIn Profile Snapshot**:
Normalized markdown of the user's current LinkedIn profile under **Career Output Root**: `output/linkedin/profile.md` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\profile.md`). Produced from paste/export landed in **Career Inbox** — not from a LinkedIn CLI or scraper by default.
_Avoid_: Scraping LinkedIn as the default intake, treating raw inbox paste as the canonical profile, inventing full profile content before the user provides material

**LinkedIn Intake**:
User-provided paste or export of LinkedIn profile material that lands in **Career Inbox** (`output/inbox/`), then is normalized into the **LinkedIn Profile Snapshot**.
_Avoid_: Official LinkedIn CLI, unofficial scrapers as default, writing the Snapshot without a user-provided source

**Profile optimization**:
Planned work by the **Real Child Skill** `optimize-linkedin-profile`: reads **LinkedIn Profile Snapshot** + **Goals Artefact** (**Hard Gate**) and proposes improvements for **Target Role** positioning in the **primary language of the existing Snapshot**. Does not auto-post or apply edits to LinkedIn.
_Avoid_: Auto-posting to LinkedIn, treating proposals as already applied, skipping the Goals Artefact hard gate, forcing a second-language rewrite of the whole profile by default

**optimize-linkedin-profile**:
Planned **Real Child Skill** (English slug) that performs **Profile optimization**. Folder not created yet. Reads Snapshot + Goals; writes proposals under Career Output Root (exact proposal file layout still open). Optimizes in the Snapshot's primary language (Career dual-track Decision B). Never posts to LinkedIn automatically.
_Avoid_: otimize-linkedin-profile, folding profile optimization into a reference-only module by default, auto-apply to LinkedIn

**Post Ideas Artefact**:
Canonical file for LinkedIn post ideas under **Career Output Root**: `output/linkedin/post-ideas.md` (full path: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\post-ideas.md`). Written by the `linkedin-post-ideas` **Reference Module**. Dated alternate files under `output/linkedin/` are allowed later if needed; preferred default path is `post-ideas.md`. May become bilingual later under Career dual-track language policy — not required in v1.
_Avoid_: Scattering post ideas outside `output/linkedin/`, inventing a full posting cadence before the module runs, auto-publishing ideas to LinkedIn, requiring bilingual post ideas before that policy is implemented

**linkedin-post-ideas**:
**Reference Module** (under `agentic-career/references/`, not a standalone skill) that drafts post ideas using **LinkedIn Profile Snapshot**, **Goals Artefact** (**Soft Gate**), and **Master CV** / **Experience Memory** as context. Writes the **Post Ideas Artefact**. Bilingual drafts are optional/later — not a hard requirement yet.
_Avoid_: Creating `.agents/skills/linkedin-post-ideas/`, treating it as a Real Child Skill, hard-blocking when goals are absent

## Relationships

- LinkedIn work shares **Career Output Root** with CV/experience skills
- **LinkedIn Intake** lands raw material in **Career Inbox**; normalization produces the **LinkedIn Profile Snapshot** at `output/linkedin/profile.md`
- `optimize-linkedin-profile` reads **LinkedIn Profile Snapshot** + **Goals Artefact** (**Hard Gate**) and proposes improvements in the Snapshot's primary language — does not auto-post to LinkedIn
- `linkedin-post-ideas` reads **LinkedIn Profile Snapshot**, **Goals Artefact** (**Soft Gate**), and **Master CV** / **Experience Memory**; writes **Post Ideas Artefact** at `output/linkedin/post-ideas.md` (bilingual later optional)
- No official LinkedIn CLI or scraper is the default intake path
- Language policy aligns with Career **CV Language Policy (dual-track)** (Career Resolved decision 16)

## Example dialogue

> **Dev:** "Should we scrape LinkedIn or use an official CLI to fill the profile?"
> **Domain expert:** "No. **LinkedIn Intake** is paste or export into **Career Inbox**, then normalize to the **LinkedIn Profile Snapshot** at `output/linkedin/profile.md`."
>
> **Dev:** "Does `optimize-linkedin-profile` push edits to LinkedIn?"
> **Domain expert:** "No. It proposes improvements from the Snapshot + **Goals Artefact** (**Hard Gate**), in the Snapshot's primary language. No auto-post."
>
> **Dev:** "Where do post ideas go, and what context does `linkedin-post-ideas` use?"
> **Domain expert:** "Preferred path: **Post Ideas Artefact** at `output/linkedin/post-ideas.md`. Context = Snapshot + goals (**Soft Gate**) + Master CV / Experience Memory. Bilingual post ideas may come later under dual-track language policy."

## Flagged ambiguities

- Exact proposal-file layout for `optimize-linkedin-profile` outputs — unresolved (skill folder not created yet).
- Snapshot section schema / field list — unresolved (path locked; do not invent full profile content).
- Posting cadence, topic taxonomy, and whether dated `post-ideas-YYYY-MM-DD.md` files are needed — unresolved (preferred default = `post-ideas.md`).
- Who performs LinkedIn Inbox → Snapshot normalization (append-data vs dedicated LinkedIn normalize step) — unresolved; storage paths locked.
- ~~**LinkedIn language vs CV dual-track**~~ — **resolved**: optimize in Snapshot primary language; post-ideas bilingual later optional. See Resolved decision 5 and Career decision 16.

## Resolved decisions

1. LinkedIn is a child area of **Agentic Career**, not a standalone memory root. Shared memory = **Career Output Root**.
2. **LinkedIn profile intake = A** — no official LinkedIn CLI / scraper as default. User provides paste or export → **Career Inbox** (`output/inbox/`) → normalize to **LinkedIn Profile Snapshot** at `output/linkedin/profile.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\profile.md`).
3. `optimize-linkedin-profile` (planned **Real Child Skill**) reads Snapshot + **Goals Artefact** (**Hard Gate**) and proposes improvements; does **not** auto-post to LinkedIn. Skill folder not created yet.
4. `linkedin-post-ideas` (**Reference Module**) uses Snapshot + goals (**Soft Gate**) + Master CV / Experience Memory; preferred write path = `output/linkedin/post-ideas.md` (full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\post-ideas.md`).
5. **Language (Career dual-track B)** — `optimize-linkedin-profile` optimizes in the **primary language of the existing LinkedIn Profile Snapshot**. **Post Ideas Artefact** may be bilingual later; not required in v1. Does not change Hybrid Artefact / `git-commits-to-cv` PT-BR-only rule. See Career Resolved decision 16.
