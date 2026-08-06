# Context Map

Mapa dos **glossários de domínio de carreira** da skill-mãe **`agentic-career`**. Vivem em `.agents/skills/portfolio/agentic-career/context/` (não na raiz do repo `agentic-ai`). Dados do usuário (memória compartilhada) vivem em `.agents/skills/portfolio/agentic-career/output/` (gitignored — só READMEs de estrutura).

O repo `agentic-ai` organiza skills por categoria em `.agents/skills/` — ver [README da categoria career](../../README.md) e o [README raiz](../../../../../README.md).

## Contexts

- [Career](./career/CONTEXT.md) — objetivos de carreira, preferências de vaga, orquestração da skill-mãe e raiz de memória compartilhada
- [CV from Commits](./cv-from-commits/CONTEXT.md) — commits git → Hybrid Artefacts de experiência (domínio da skill `git-commits-to-cv`)
- [LinkedIn](./linkedin/CONTEXT.md) — Profile Snapshot, intake via Career Inbox, profile optimization e post ideas; compartilha a mesma Career Output Root

## Relationships

- **Career → CV from Commits / LinkedIn**: Career define **Career Output Root**, **Experience Memory**, e **Master CV**; skills filhas leem/escrevem nessa memória compartilhada
- **CV from Commits → Career**: produz **Hybrid Artefacts** em **Experience Memory** (`output/experience/`); não consolida o CV final
- **Career Consolidation**: `summarize-into-doc` (Phase 1) lê XYZ de **Experience Memory** → escreve **Master CV** + **Master CV EN** (`output/cv/master_cv.md`, `master_cv.en.md`); não atualiza o Portfolio CV
- **LinkedIn ↔ Career**: paste/export → **Career Inbox** → **LinkedIn Profile Snapshot** (`output/linkedin/profile.md`); `optimize-linkedin-profile` / `linkedin-post-ideas` = Phase 2

## Mother skill

- Skill: `.agents/skills/portfolio/agentic-career/`
- Shared memory: `.agents/skills/portfolio/agentic-career/output/`
- Experience artefacts: `.agents/skills/portfolio/agentic-career/output/experience/`
- Career Inbox (raw, gitignored): `.agents/skills/portfolio/agentic-career/output/inbox/`
- Master CV (PT + EN): `.agents/skills/portfolio/agentic-career/output/cv/master_cv.md`, `master_cv.en.md`
- LinkedIn Profile Snapshot: `.agents/skills/portfolio/agentic-career/output/linkedin/profile.md`
- Post Ideas Artefact: `.agents/skills/portfolio/agentic-career/output/linkedin/post-ideas.md`
- **Phase 1 (choice A)**: mother skill + `references/` for `goals-intake`, `append-data-to-cv`, `summarize-into-doc` (+ `cv-happy-path`); sibling Real Child Skill `git-commits-to-cv`. **Phase 2 deferred**: `optimize-linkedin-profile`, `adapt-cv-to-job`, full `linkedin-post-ideas`, study/companies content, `applications.md`. Details: [career/CONTEXT.md](./career/CONTEXT.md) decision 18.
