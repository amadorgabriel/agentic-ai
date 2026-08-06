# summarize-into-doc — Consolidation → Master CV (+ EN)

**Reference Module** (não é skill standalone). **Consolidation**: lê **XYZ Bullets** de **Experience Memory** (+ **Goals Artefact** como Soft Gate) e escreve **Master CV** PT + **Master CV EN**.

Fonte: [context/career/CONTEXT.md](../context/career/CONTEXT.md) (Resolved 9, 16). Não escreve **Portfolio CV**.

## Quando rodar

- Usuário pede consolidar / gerar master CV / “atualizar master_cv”
- **Pipeline A** passo 4 (após append/git conforme aplicável)
- Sempre com **Heavy-step Confirmation** antes de reescrever masters existentes

## Paths (únicos write targets)

| Artefacto | Path |
| --- | --- |
| Master CV (PT) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.md` |
| Master CV EN | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\cv\master_cv.en.md` |
| Experience Memory (read) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\**\*.md` |
| Goals (read, soft) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\goals.md` |

### NUNCA escrever

- `c:\_git\projects\portfolio\public\assets\pdf\current_cv.md` (**Portfolio CV**)
- Hybrid Artefacts em inglês / reescrever `experience/` para EN
- Tailored CVs (`master_cv.<job-slug>.md`) — isso é `adapt-cv-to-job` (Phase 2)
- Raw inbox como se fosse experiência canônica

## Checklist rápido

```
summarize-into-doc progress:
- [ ] 1. Soft Gate goals
- [ ] 2. Inventariar artefactos em experience/
- [ ] 3. Selecionar XYZ (não STAR) por empresa/projeto
- [ ] 4. Confirmar com usuário ANTES de rewrite se masters existem
- [ ] 5. Escrever master_cv.md (PT) — ATS
- [ ] 6. Escrever master_cv.en.md (EN) traduzindo XYZ — sem tocar artefacts
- [ ] 7. Resumir diffs / placeholders remanescentes
```

## Passo 1 — Soft Gate

Se `goals.md` ausente: avisar + oferecer [goals-intake.md](goals-intake.md). Pode continuar com defaults do glossário (Fullstack/Frontend Pleno; SP híbrido-remoto / LATAM HO; >10k BRL) para framing do sumário/headline — **não** inventar emprego ou métricas.

## Passo 2 — Inventário

Listar todos os Hybrid Artefacts sob `output/experience/`. Para cada um, extrair:

- company-slug / project-slug / título
- período (se houver nos metadados ou notas)
- bullets da seção **Bullets XYZ (CV)** apenas
- placeholders `[MÉTRICA A CONFIRMAR]` ainda abertos

**Ignorar** por padrão a seção STAR na prosa do Master (STAR = entrevista).

Se `experience/` estiver vazio: parar e orientar append e/ou `git-commits-to-cv` — não inventar master.

## Passo 3 — Confirmação obrigatória (Heavy-step)

Antes de escrever/sobrescrever masters, mostrar plano curto:

1. Empresas/projetos que entrarão
2. Quantidade aproximada de bullets por bloco
3. Se `master_cv.md` / `master_cv.en.md` já existem → deixar claro que serão **reescritos** (ou pedir política: replace total vs seções)

**Só continuar após OK explícito do usuário.**

## Passo 4 — Estrutura ATS (PT primeiro)

Ordem recomendada de `master_cv.md`:

```markdown
# <Nome>

## Contato
<!-- só o que o usuário já forneceu / confirmou; não inventar telefone/endereço -->

## Sumário profissional
<!-- 2–4 linhas; alinhado a goals ou defaults do glossário; sem métricas inventadas -->

## Experiência
### <Empresa> — <Papel se conhecido>
*<período se conhecido>*

- <bullet XYZ>
- …

### …

## Projetos relevantes
<!-- opcional: se engajamentos forem melhor lidos fora do bloco Experiência -->

## Stack / competências
<!-- keywords reais evidenciadas nos artefactos; sem lista fantasiosa -->

## Formação
<!-- só se houver dado confirmado do usuário ou fonte prévia; senão omitir ou pedir -->

## Idiomas / outros
<!-- opcional -->
```

### Regras de consolidação

1. **PT-BR** no `master_cv.md`.
2. Uma linha por bullet; verbo/impacto claros (ATS).
3. Preferir 3–6 XYZ por empresa/projeto no Master (curadoria) — se o artefacto tem 8, escolher os mais fortes alinhados ao Target Role / goals; não dump cego.
4. Manter `[MÉTRICA A CONFIRMAR]` se ainda não confirmado — **não** fabricar Y na Consolidation.
5. Não copiar longos blocos STAR para o Master.
6. Não reescrever os Hybrid Artefacts.
7. Não sincronizar Portfolio CV.

## Passo 5 — Master CV EN

Após (ou em seguida ao) PT estável:

1. Gerar `master_cv.en.md` com a **mesma estrutura**.
2. Traduzir/adaptar sumário + bullets XYZ para inglês natural de CV (não word-for-word tosco).
3. Keywords técnicas podem permanecer quando forem nomes próprios (React, .NET, OCPP).
4. **Não** alterar arquivos em `experience/`.
5. Placeholders: usar `[METRIC TO CONFIRM]` no EN **ou** manter o marcador PT de forma consistente — preferir `[METRIC TO CONFIRM]` no EN e listar no resumo final o mapeamento para os itens PT abertos.

Só inventar `master_cv.en.md` quando esta Consolidation rodar (não criar EN vazio antes).

## Passo 6 — Encerrar

Entregar ao usuário:

- Paths dos dois masters
- Contagem de bullets / empresas incluídas
- Lista de métricas ainda placeholder
- Lembrete: sync para Portfolio CV = futuro **publish-cv** (fora de escopo)
- Phase 2: `adapt-cv-to-job` para variantes por vaga

## Hard rules

| Do | Don't |
| --- | --- |
| Escrever só `output/cv/master_cv.md` + `master_cv.en.md` | Escrever `portfolio/.../current_cv.md` |
| Confirmar antes de rewrite | Sobrescrever Master em silêncio |
| Ler `experience/` (+ goals soft) | Tratar inbox raw como experiência |
| Traduzir XYZ só no EN master | Reescrever artefacts em EN |
| Curadoria ATS | Dump STAR / changelog |
| Preservar placeholders honestos | Inventar métricas na Consolidation |
