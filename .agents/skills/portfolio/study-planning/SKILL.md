---
name: study-planning
description: >-
  Orquestra roadmap de estudos para Senior Full Stack Developer (React/Next.js,
  ASP.NET Core, Cloud/DevOps, IA aplicada), Company Shortlist e Study Plan
  alinhados a goals/JD. Mantém progresso persistente, sugere próximo tópico e
  conduz sessões de estudo. Use quando o usuário invocar study-planning, pedir
  roadmap/plano de estudos, marcar progresso, escolher próximo tópico, shortlist
  de empresas ou estudar stack fullstack React + .NET + IA. Não use para
  CV/LinkedIn (summarize-cv, optimize-linkedin) nem implementação em produção
  (tlc-spec-driven).
disable-model-invocation: true
---

# Study Planning — Fullstack Senior (React + .NET + IA)

Roadmap técnico em 8 fases (0–7), **Company Shortlist** e **Study Plan** personalizado.

Categoria: **portfolio** — ver [README da categoria](../README.md).

Sibling skills (invocar separadamente; não executar aqui):

- [`summarize-cv`](../summarize-cv/SKILL.md) — goals, Tailored CV com JD Summary
- [`git-commits-to-cv`](../git-commits-to-cv/SKILL.md) — consolidar prática em Experience Memory
- [`tlc-spec-driven`](../../engineering/tlc-spec-driven/SKILL.md) — projetos práticos grandes
- [`domain-modeling`](../../engineering/domain-modeling/SKILL.md) — prática DDD/ADR
- [`grilling`](../../engineering/grilling/SKILL.md) — stress-test antes de marcar tópico como solid
- [`optimize-linkedin`](../_/optimize-linkedin/SKILL.md) — stub local (gitignored)

Glossário CV: [summarize-cv/dictionary/cv/CONTEXT.md](../summarize-cv/dictionary/cv/CONTEXT.md) — termos **Company Shortlist**, **Study Plan**, **JD Summary**.

## When to use / routing

| Intent | Route |
| --- | --- |
| Estudar, roadmap, progresso, próximo tópico | Esta skill |
| Shortlist de empresas (BR/LATAM) | [references/company-shortlist.md](references/company-shortlist.md) |
| Plano de estudo a partir de JD/gaps | [references/jd-gap-analysis.md](references/jd-gap-analysis.md) |
| Otimizar/adaptar CV | `summarize-cv` |
| Implementar feature real | `tlc-spec-driven` |
| LinkedIn | stub `portfolio/_/optimize-linkedin` |

## Quick start

1. Ler ou criar artefatos em `output/` (ver Output root abaixo)
2. Ler [ROADMAP.md](ROADMAP.md) para ordem canônica do currículo técnico
3. Se existir Tailored CV ou `summarize-cv/output/goals.md`, cruzar gaps → [references/jd-gap-analysis.md](references/jd-gap-analysis.md)
4. Identificar fase/tópico atual; sugerir **um** próximo passo
5. Conduzir sessão → [references/session-workflow.md](references/session-workflow.md)
6. Atualizar `output/progress.md` (e `output/study/plan.md` se relevante) ao encerrar

## Roadmap (visão)

| Fase | Nome | Reference |
| --- | --- | --- |
| 0 | Ferramentas & Base | [phase-0-tools-base.md](references/phase-0-tools-base.md) |
| 1 | Fundamentos | [phase-1-fundamentals.md](references/phase-1-fundamentals.md) |
| 2 | Engenharia base | [phase-2-engineering-base.md](references/phase-2-engineering-base.md) |
| 3 | Frontend | [phase-3-frontend.md](references/phase-3-frontend.md) |
| 4 | Backend .NET | [phase-4-backend-dotnet.md](references/phase-4-backend-dotnet.md) |
| 5 | Cloud & DevOps | [phase-5-cloud-devops.md](references/phase-5-cloud-devops.md) |
| 6 | IA Aplicada | [phase-6-applied-ai.md](references/phase-6-applied-ai.md) |
| 7 | Produto & Mensuração | [phase-7-product-metrics.md](references/phase-7-product-metrics.md) |

Postergados: [DEFERRED.md](DEFERRED.md) — não sugerir como próximo passo.

## Session modes

| Modo | Quando | Ação |
| --- | --- | --- |
| **Discover** | Usuário novo | Intake rápido → criar `output/progress.md` |
| **Continue** | Sessão retomada | Ler progress → retomar tópico `in_progress` |
| **Deep dive** | Tópico específico | Carregar reference da fase; teoria + exercício |
| **Checkpoint** | Validação pedida | Quiz ou grilling leve → atualizar status |
| **Project** | Tópico precisa prática | Mini-projeto; opcionalmente `tlc-spec-driven` |
| **JD align** | Tailored CV / vaga | Mapear gaps JD → tópicos do roadmap |

## Progress rules

- Fonte de verdade do roadmap: `output/progress.md`
- Status por item: `not_started` | `in_progress` | `practice` | `solid` | `deferred`
- Não marcar `solid` sem confirmação ou evidência (projeto, quiz, grilling)
- Um próximo tópico por sessão
- Registrar data ao mudar para `solid`
- Itens em [DEFERRED.md](DEFERRED.md) só com pedido explícito

## Output root

```
.agents/skills/portfolio/study-planning/output/
├── progress.md              # Progresso do roadmap técnico
├── study/
│   └── plan.md              # Study Plan (prioridades, gaps JD, metas)
├── companies/
│   ├── br.md                # Company Shortlist — Brasil
│   └── latam.md             # Company Shortlist — LATAM/exterior HO
├── session-log/             # Notas por sessão (opcional)
└── projects/                # Links/descrição de projetos práticos
```

Pode **ler** `summarize-cv/output/goals.md` e Tailored CV (JD Summary). Não escrever em `summarize-cv/output/`.

Template inicial: [templates/progress.template.md](templates/progress.template.md)

## Hard rules

- Invocação explícita apenas
- Não executar pipeline CV aqui
- Não incluir itens de DEFERRED.md em próximos passos
- Carregar reference de fase sob demanda (não todas de uma vez)
- Preferir docs oficiais sobre memória do modelo para APIs específicas
- Company Shortlist e Study Plan vivem só em `study-planning/output/`

## References

- [ROADMAP.md](ROADMAP.md)
- [DEFERRED.md](DEFERRED.md)
- [references/session-workflow.md](references/session-workflow.md)
- [references/company-shortlist.md](references/company-shortlist.md)
- [references/jd-gap-analysis.md](references/jd-gap-analysis.md)
- [references/phase-*.md](references/)
