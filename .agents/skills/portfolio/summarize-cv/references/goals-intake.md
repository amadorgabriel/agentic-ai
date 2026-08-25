# goals-intake — Goals Artefact

**Reference Module** (não é skill standalone). Escreve/atualiza o **Goals Artefact** em `output/goals.md` via autoquestionamento + **Smart Merge**.

Fonte de decisões: [dictionary/cv/CONTEXT.md](../dictionary/cv/CONTEXT.md) (Resolved 10, 11). Defaults de glossário: **Target Role**, **Location Preference**, **Comp Floor**.

## Quando rodar

- Usuário pede intake / “definir objetivos” / “atualizar goals”
- **Pipeline A** passo 1 quando `output/goals.md` falta (**Soft Gate** — oferecer; pode continuar sem)
- Antes de um **Hard Gate** (`adapt-cv-to-job`, sibling `optimize-linkedin`) — preparar/exigir o artefacto

## Path de saída

```
.agents/skills/portfolio/summarize-cv/output/goals.md
```

Não inventar stub antes do intake. Não gravar respostas live em `dictionary/cv/CONTEXT.md`.

## Checklist rápido

```
goals-intake progress:
- [ ] 1. Ler goals.md se existir (planejar Smart Merge)
- [ ] 2. Autoquestionar campos faltantes / a confirmar
- [ ] 3. Validar vs defaults do glossário (avisar divergências)
- [ ] 4. Escrever ou Smart Merge goals.md
- [ ] 5. Resumir o que ficou confirmado vs aberto
```

## Campos obrigatórios (mínimo útil)

| Campo | Pergunta-guia | Default glossário (se Soft Gate seguir sem arquivo) |
| --- | --- | --- |
| `target_roles` | Quais cargos/títulos você está mirando agora? | Eng. Software Fullstack Pleno, Frontend Pleno, correlatos |
| `location` | Híbrido/remoto SP, 100% HO exterior (LATAM?), on-site? | Híbrido/remoto SP; exterior 100% HO com prioridade LATAM |
| `comp_floor` | Piso salarial mensal (BRL ou equivalente)? | >10k BRL/mês |
| `constraints` | O que é deal-breaker? (stack, setor, CLT/PJ, viagem, idioma…) | — (só o que o usuário disser) |
| `positioning` | Como você quer ser lido em 1–2 frases? (hipótese de posicionamento) | — |

Campos opcionais úteis: `timeline` (quando quer mudar), `must_have_stack`, `nice_to_have`, `avoid_list` (empresas/setores a evitar), `notes`.

## Roteiro de autoquestionamento (PT-BR)

Fazer **uma pergunta por vez** (ou no máximo um bloco curto de 2–3 se o usuário pedir ritmo rápido). Não bombardear com questionário longo.

1. **Papéis** — “Quais títulos você aceitaria nas próximas candidaturas? (ex.: Fullstack Pleno, Frontend Pleno, correlatos)”
2. **Local** — “Preferência de arranjo: híbrido/remoto em SP, 100% remoto no exterior (LATAM?), ou outra?”
3. **Comp** — “Qual o piso mensal aceitável (BRL ou moeda + conversão aproximada)?”
4. **Constraints** — “Há restrições duras? (PJ/CLT, stack mínima, setor, viagem, inglês obrigatório…)”
5. **Positioning** — “Se um recrutador ler seu CV em 10s, qual hipótese de posicionamento você quer reforçar?”
6. **Opcionais** — timeline, stacks must/nice, avoid-list — só se o usuário engajar.

Se o usuário responder “usa os defaults do glossário”, preencher `target_roles` / `location` / `comp_floor` com os defaults e marcar `source_of_defaults: glossary` nesses campos.

## Smart Merge (re-run)

Quando `goals.md` **já existe**:

1. Ler o arquivo completo.
2. **Preservar** respostas marcadas como confirmadas (`confirmed: true` ou checklist marcado).
3. **Perguntar só** campos vazios, `confirmed: false`, ou onde o usuário pediu revisão.
4. **Não** sobrescrever confirmações com defaults do glossário sem OK explícito.
5. Atualizar `updated_at`; manter `created_at`.

### Anti-padrões

| Evitar | Fazer |
| --- | --- |
| Apagar goals confirmados | Merge campo a campo |
| Inventar constraints/posicionamento | Deixar vazio ou perguntar |
| Espelhar glossário em `dictionary/cv/CONTEXT.md` | Só em `output/goals.md` |
| Criar stub vazio “para depois” | Só escrever após pelo menos um turno de intake |

## Template de saída

```markdown
# Goals Artefact

## Metadados

| Campo | Valor |
| --- | --- |
| created_at | `<ISO-8601 UTC>` |
| updated_at | `<ISO-8601 UTC>` |
| política | Smart Merge |
| glossário de referência | dictionary/cv/CONTEXT.md — Target Role / Location Preference / Comp Floor |

## Objetivos confirmados

### Papéis-alvo (`target_roles`)

- …

<!-- confirmed: true|false -->

### Localização / arranjo (`location`)

- …

### Piso de compensação (`comp_floor`)

- … <!-- ex.: >10k BRL/mês -->

### Constraints (`constraints`)

- …

### Posicionamento (`positioning`)

- …

## Opcionais

| Campo | Valor |
| --- | --- |
| timeline | … |
| must_have_stack | … |
| nice_to_have | … |
| avoid_list | … |
| notes | … |

## Checklist de validação

- [ ] Papéis-alvo batem com o que quero nas próximas 4–8 semanas
- [ ] Piso de comp está atualizado (moeda / conversão)
- [ ] Constraints duras estão listadas (nada crítico omitido)
- [ ] Frase de posicionamento serve para CV + LinkedIn

## Notas de merge (só em re-runs)

- Preservado: …
- Atualizado: …
- Perguntado ao usuário: …
```

## Encerrar

Resumir ao usuário:

- Path escrito/atualizado
- Campos confirmados vs abertos no checklist
- Lembrete Soft Gate: Consolidation / append / git-commits podem seguir com defaults do glossário se o usuário optar por não completar agora
