# JD Gap Analysis

**Trigger:** Tailored CV criado, "gaps da vaga", "o que estudar para essa JD"

## Inputs

1. **JD Summary** embutido no Tailored CV (`summarize-cv/output/cv/master_cv.<job-slug>.md`)
2. Raw JD em `summarize-cv/output/inbox/` (se precisar de detalhe)
3. `output/progress.md` — o que já está `solid` ou `practice`
4. [ROADMAP.md](../ROADMAP.md) — mapa de tópicos

## Output

Atualizar `output/study/plan.md`:

```markdown
# Study Plan

**Atualizado:** YYYY-MM-DD
**Contexto:** master_cv.<job-slug> | goals | roadmap geral

## Prioridades (próximas 2–4 semanas)

1. [Tópico roadmap] — gap JD: "…" — status atual: …
2. …

## Gaps mapeados

| JD requirement | Roadmap topic | Status | Ação |
| --- | --- | --- | --- |
| … | … | … | … |

## Backlog (após prioridades)

- …

## Projetos sugeridos

- …
```

## Process

1. Extrair must-haves e nice-to-haves da JD Summary
2. Mapear cada item para tópico(s) do ROADMAP (fuzzy match ok — confirmar com usuário)
3. Comparar com `progress.md` — gaps = JD exige e status ≠ `solid`
4. Ordenar por: must-have > frequência em shortlist > fase do roadmap
5. Escrever 3–5 prioridades acionáveis (não lista enorme)
6. Sugerir próxima sessão via [session-workflow.md](session-workflow.md)

## Integration

- Se não houver Tailored CV: oferecer `summarize-cv` → adapt-cv-to-job primeiro
- Gaps consolidados alimentam Company Shortlist (fit/gaps por empresa)
