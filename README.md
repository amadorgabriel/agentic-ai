# agentic-ai

Vitrine das minhas **skills de agentes de IA** — workflows reutilizáveis para Cursor, Claude Code e ferramentas compatíveis.

> **Descrição sugerida (GitHub About):**  
> Vitrine de skills de agentes de IA: engenharia, portfolio e job-related — workflows reutilizáveis para Cursor/Claude.

## Estrutura

```
.agents/skills/
├── engineering/   # skills de desenvolvimento
├── portfolio/     # carreira, CV, LinkedIn, portfólio
├── job-related/   # emprego atual
└── deprecated/    # arquivo histórico — agentes devem ignorar
```

Cada categoria tem um `README.md` explicando o propósito. Skills ativas têm um `SKILL.md` na pasta da skill.

## Categorias

| Categoria | O que tem |
| --- | --- |
| [engineering](.agents/skills/engineering/) | Code review, spec-driven, grilling, autofix… |
| [portfolio](.agents/skills/portfolio/) | `summarize-cv`, `git-commits-to-cv`, `cv-md-to-docx` (+ stubs locais em `portfolio/_/`) |
| [job-related](.agents/skills/job-related/) | Skills do dia a dia no emprego |
| [deprecated](.agents/skills/deprecated/) | Skills antigas (não usar) |

## Como os agentes devem se comportar

Ver [AGENTS.md](./AGENTS.md): carregar só skills ativas; **nunca** usar `deprecated/`.

## Licença

[MIT](./LICENSE)
