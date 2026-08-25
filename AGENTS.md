# AGENTS

Regras para agentes que trabalham neste repositório.

## Onde vivem as skills

Skills ativas ficam em `.agents/skills/<categoria>/<nome-da-skill>/SKILL.md`.

Categorias ativas:

| Pasta | Uso |
| --- | --- |
| `engineering/` | Desenvolvimento de software |
| `portfolio/` | Carreira, CV, LinkedIn e portfólio |
| `job-related/` | Contexto do emprego atual |

## Ignorar `deprecated/`

**Nunca carregue, sugira ou execute skills em `.agents/skills/deprecated/`.**

Essa pasta é só arquivo histórico. Os manifests foram renomeados de `SKILL.md` para `ARCHIVED.md` de propósito, para os agentes não descobrirem essas skills automaticamente.

## Descoberta

- Cursor / Claude Code / ferramentas compatíveis varrem `.agents/skills/**/SKILL.md`.
- Skills sob `_/` (gitignored) são locais ao job atual e não fazem parte da vitrine pública.
- Outputs pessoais de carreira em `portfolio/<skill>/output/` e stubs locais em `portfolio/_/` são gitignored.
