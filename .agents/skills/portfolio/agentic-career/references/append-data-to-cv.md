# append-data-to-cv — Inbox → Experience Memory

**Reference Module** (não é skill standalone). Aterra material bruto no **Career Inbox**, normaliza em **Hybrid Artefacts** sob **Experience Memory**, com **Artefact Source** `manual` \| `cv-import` \| `doc`.

Fonte: [context/career/CONTEXT.md](../context/career/CONTEXT.md) (Resolved 12). Template de artefacto: [git-commits-to-cv/references/artefact-template.md](../../git-commits-to-cv/references/artefact-template.md). Métodos XYZ/STAR: [git-commits-to-cv/references/methods.md](../../git-commits-to-cv/references/methods.md).

## Quando rodar

- Usuário cola CV antigo, write-up de projeto, notes, export, PDF texto, etc.
- **Pipeline A** passo 2 quando `output/inbox/` tem itens **ou** o usuário diz que tem material
- Soft Gate em `goals.md`: avisar + oferecer intake; pode continuar

## Paths

| Papel | Path |
| --- | --- |
| Career Inbox (raw) | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\inbox\` |
| Experience Memory | `c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\<company-slug>\<project-slug>.md` |

Inbox é **gitignored** (PII) — só `inbox/README.md` versionado. Nunca tratar inbox como experiência canônica para Consolidation.

## Checklist rápido

```
append-data-to-cv progress:
- [ ] 1. Soft Gate goals (avisar se goals.md ausente)
- [ ] 2. Aterrar raw no inbox (nomear arquivo)
- [ ] 3. Classificar source: manual | cv-import | doc
- [ ] 4. Extrair conquistas → XYZ (+ STAR opcional) PT-BR
- [ ] 5. Resolver company-slug / project-slug
- [ ] 6. Escrever ou Smart Merge Hybrid Artefact
- [ ] 7. Marcar item do inbox como processado (nota no raw ou resumo)
```

## Passo 1 — Soft Gate

Se `output/goals.md` não existir: avisar, oferecer [goals-intake.md](goals-intake.md). Se o usuário seguir, usar defaults do glossário só para framing (não inventar fatos de experiência).

## Passo 2 — Aterrar no inbox

1. Pedir/aceitar o material (paste ou path de arquivo).
2. Gravar em `output/inbox/` com nome estável:

```
YYYY-MM-DD_<kind>_<short-slug>.md
```

Exemplos:

- `2026-08-06_cv-import_curriculo-antigo.md`
- `2026-08-06_doc_spott-case-study.md`
- `2026-08-06_manual_notas-etiqueta-certa.md`

3. Se o usuário colar só no chat: criar o `.md` no inbox com o texto (não deixar só na conversa).
4. Prefácio curto no topo do raw (opcional):

```markdown
---
kind: cv-import   # manual | cv-import | doc
received_at: <ISO-8601>
status: pending   # pending | normalized | skipped
notes: …
---
```

**Não** normalizar LinkedIn Profile Snapshot neste módulo na Phase 1 (Phase 2 / ownership TBD). Se o material for claramente perfil LinkedIn, aterrar no inbox e avisar que Snapshot (`output/linkedin/profile.md`) é fluxo Phase 2 — não inventar `profile.md` completo aqui salvo pedido explícito futuro.

## Passo 3 — Escolher Artefact Source

| Source | Quando |
| --- | --- |
| `cv-import` | CV/résumé completo ou grande bloco de experiência laboral |
| `doc` | Case study, README de projeto, post mortem, design doc, portfolio write-up |
| `manual` | Notas soltas, bullets ditados, correções pontuais do usuário |

`git` é **somente** de `git-commits-to-cv` — nunca setar `git` neste módulo.

## Passo 4 — Normalizar para Hybrid Artefact

1. Ler o raw do inbox.
2. Identificar empresa/cliente + projeto/engajamento → propor `company-slug` e `project-slug` (kebab-case); confirmar com o usuário se ambíguo.
3. Extrair **5–8** conquistas de topo (ou menos se a fonte for curta — não inventar para encher).
4. Redigir **XYZ Bullets** em **PT-BR** (fórmula Google XYZ). Métodos → sibling `methods.md`.
5. **STAR Notes** opcionais mas recomendadas quando houver contexto suficiente.
6. Métricas: **NUNCA inventar**. Usar `[MÉTRICA A CONFIRMAR]` + Validation Checklist.
7. Preencher o template Hybrid Artefact (sibling `artefact-template.md`) com:
   - `source` = `manual` \| `cv-import` \| `doc`
   - campos git (`Scanned repository`, `Commit Window`, `Emails`) = `N/A` ou omitir
   - `Target Role Bias` default Fullstack Engineer Pleno (ou override do usuário / goals)
8. Path de saída: `output/experience/<company-slug>/<project-slug>.md`

### CV-import: fatiar por empresa/projeto

Um CV antigo costuma gerar **vários** artefactos (um por projeto ou um por empresa+projeto). Não despejar o CV inteiro num único arquivo se houver múltiplos engajamentos claros. Pedir confirmação do mapa:

```
Proposta de artefactos:
1. etiqueta-certa / ec-v3-ui  (source: cv-import)
2. spott / spott-server       (source: cv-import)
…
```

## Passo 5 — Smart Merge

Se o artefacto já existe (ex.: veio de `git-commits-to-cv`):

1. Ler artefacto atual.
2. **Preservar** métricas confirmadas e STAR existentes.
3. **Fundir** bullets novos do material manual/doc **sem** apagar evidência git sólida.
4. Em conflito de claim: perguntar (não silenciar).
5. Atualizar `Última atualização`, `source` se a run for predominantemente não-git — ou anotar em “Notas de merge” que houve contribuição `cv-import`/`manual`/`doc` mantendo `source: git` se o artefacto nasceu do git e o usuário quiser preservar proveniência primária.

Regra prática de `source` em merge misto:

- Artefacto novo só deste módulo → `source` = manual|cv-import|doc
- Artefacto existente `source: git` → manter `git` no metadado principal; registrar proveniência adicional nas Notas de merge
- Não apagar hashes/evidência de commits

## Passo 6 — Encerrar item do inbox

- Atualizar frontmatter do raw: `status: normalized` + lista de paths de artefactos escritos
- Ou, se o usuário pedir skip: `status: skipped` + motivo

## Hard rules

| Do | Don't |
| --- | --- |
| Raw → inbox primeiro | Escrever Hybrid só no chat / só no inbox |
| XYZ PT-BR no `experience/` | EN no artefacto; bilingual sections |
| `source` manual\|cv-import\|doc | `source: git` neste módulo |
| Smart Merge com artefactos existentes | Blind overwrite de métricas/STAR confirmadas |
| Placeholder de métrica | Inventar % / latência / receita |
| Soft Gate goals | Hard-bloquear Consolidation path por goals ausente |

## Encerrar

Resumir:

- Arquivos criados/atualizados em `experience/`
- Itens inbox `normalized` / `pending` / `skipped`
- Placeholders abertos no Validation Checklist
- Próximo passo natural: Consolidation ([summarize-into-doc.md](summarize-into-doc.md)) — com confirmação antes de reescrever Master
