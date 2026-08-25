# Template — Hybrid Memory Artefact

Path: `.agents/skills/portfolio/summarize-cv/output/experience/<company-slug>/<project-slug>.md`

Fill every section. Language: **PT-BR only**. Replace placeholders in `<angle brackets>`.

```markdown
# <Nome do projeto / engajamento>

## Metadados

| Campo | Valor |
| --- | --- |
| company-slug | `<company-slug>` |
| project-slug | `<project-slug>` |
| source | `git` \| `manual` \| `cv-import` \| `doc` |
| Scanned repository | `<absolute-path>` <!-- omit/N/A when source ≠ git --> |
| Commit Window | `<YYYY-MM-DD>` → `<YYYY-MM-DD>` (ou descrição do período de emprego) <!-- omit/N/A when source ≠ git --> |
| Emails usados | `<lista allowlist efetiva desta run>` <!-- omit/N/A when source ≠ git --> |
| Target Role Bias | `Fullstack Engineer Pleno` \| `Frontend Pleno` \| `neutral` |
| Gerado em | `<ISO-8601 UTC>` |
| Última atualização | `<ISO-8601 UTC>` |
| Política de re-run | Smart Merge |

## Bullets XYZ (CV)

> 5–8 conquistas de topo. Formato: conquistou **X** medido por **Y** fazendo **Z**.
> Se Y não tiver evidência: use `[MÉTRICA A CONFIRMAR]`.

1. …
2. …
3. …
4. …
5. …
<!-- até 8 -->

## Notas STAR (entrevista)

### Conquista 1 — <título curto alinhado ao bullet XYZ #1>

- **S (Situação):** …
- **T (Tarefa):** …
- **A (Ação):** …
- **R (Resultado):** … <!-- use [MÉTRICA A CONFIRMAR] se necessário -->

### Conquista 2 — <título curto>

- **S:** …
- **T:** …
- **A:** …
- **R:** …

<!-- uma nota STAR por bullet XYZ relevante -->

## Checklist de validação

Itens que o usuário deve confirmar antes de tratar métricas/claims como finais:

- [ ] `[MÉTRICA A CONFIRMAR]` em bullet #N — contexto: …
- [ ] Claim sem evidência forte em commits — bullet #N: …
- [ ] Período de emprego / Commit Window conferido
- [ ] Emails incluídos nesta run estão corretos
- [ ] Nenhum trabalho inventado fora do histórico git

## Evidência de commits (opcional)

| Tema / conquista | Hashes (amostra) | Notas |
| --- | --- | --- |
| `<tema>` | `abc1234`, `def5678` | … |

## Notas de merge (só em re-runs)

- Preservado: métricas confirmadas — …
- Preservado: STAR — …
- Atualizado a partir de nova evidência — …
- Ambiguidades perguntadas ao usuário — …
```
