# Company Shortlist

**Trigger:** "empresas", "shortlist", "onde aplicar", "targets BR/LATAM"

## Outputs

| Arquivo | Escopo |
| --- | --- |
| `output/companies/br.md` | Brasil — híbrido/remoto SP |
| `output/companies/latam.md` | Exterior 100% HO — prioridade LATAM |

## Defaults (do glossário CV)

- **Target roles:** Fullstack Pleno/Sênior, Frontend Pleno/Sênior, correlatos
- **Location:** híbrido/remoto SP, ou exterior 100% HO com prioridade LATAM
- **Comp floor:** >10k BRL/mês (ou equivalente)

Ler `summarize-cv/output/goals.md` se existir — goals override defaults.

## Company Entry template

Por empresa:

```markdown
### [Nome] — Tier [A|B|C]

- **Stack:** React, .NET, …
- **Modalidade:** remoto / híbrido / presencial
- **Comp (est.):** …
- **Fit:** alto | médio | exploratório
- **Gaps vs perfil:** …
- **Links:** careers page, LinkedIn, …
- **Status:** research | applied | interview | rejected | offer
```

**Tier A:** fit forte + stack alinhada + comp ok  
**Tier B:** fit bom com gaps estudáveis  
**Tier C:** exploratório / long shot

## Workflow

1. Confirmar goals/location/comp floor
2. Ler shortlists existentes
3. Adicionar/atualizar entradas com evidência (não inventar salários)
4. Cruzar gaps com [ROADMAP.md](../ROADMAP.md) → priorizar estudo
5. Se houver Tailored CV ativo, alinhar shortlist à vaga

## Hard rules

- Shortlist vive só em `study-planning/output/companies/`
- Não duplicar em `summarize-cv/output/`
- Não commitar dados pessoais sensíveis além do gitignored output
