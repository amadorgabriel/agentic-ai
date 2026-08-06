# LinkedIn output

Subtree of **Career Output Root** for LinkedIn-related artefacts.

Path: `.agents/skills/portfolio/agentic-career/output/linkedin/`

## Canonical paths

| Path | Artefact | Role |
| --- | --- | --- |
| `profile.md` | **LinkedIn Profile Snapshot** | Normalized current LinkedIn profile. Full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\profile.md` |
| `post-ideas.md` | **Post Ideas Artefact** | Preferred file for LinkedIn post ideas. Full: `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\linkedin\post-ideas.md` |

Dated alternate files under this directory (e.g. `post-ideas-YYYY-MM-DD.md`) may be used later if needed; the preferred default remains `post-ideas.md`.

## Intake (Decision A)

1. User provides LinkedIn **paste or export** (no official LinkedIn CLI / scraper as default).
2. Raw material lands in **Career Inbox**: `../inbox/`.
3. Normalize into the **LinkedIn Profile Snapshot** at `profile.md`.

Do **not** invent full profile content in `profile.md` before the user provides material. Paths are documented; files may be absent until intake/normalize runs.

## Consumers

| Step | Kind | Reads | Writes | Notes |
| --- | --- | --- | --- | --- |
| `optimize-linkedin-profile` | Planned Real Child Skill | Snapshot + **Goals Artefact** (**Hard Gate**) | Improvement proposals (layout TBD) | Does **not** auto-post to LinkedIn. Skill folder not created yet. |
| `linkedin-post-ideas` | Reference Module | Snapshot + goals (**Soft Gate**) + Master CV / Experience Memory | `post-ideas.md` (preferred) | Under `agentic-career/references/` only |

## Related

- LinkedIn context: [context/linkedin/CONTEXT.md](../../context/linkedin/CONTEXT.md)
- Career context: [context/career/CONTEXT.md](../../context/career/CONTEXT.md) (Resolved decision 13)
- Career Inbox: [../inbox/README.md](../inbox/README.md)
- Output root: [../README.md](../README.md)
