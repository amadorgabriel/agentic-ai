# cv-happy-path — Pipeline A (orquestração)

Helper de **summarize-cv**. Orquestra o **CV Happy Path** (**Pipeline A**) com Soft Gate em goals e **Heavy-step Confirmation** antes de git scan e rewrite do Master.

Fonte: [dictionary/cv/CONTEXT.md](../dictionary/cv/CONTEXT.md) Resolved decision 17–19. Entrada principal: [SKILL.md](../SKILL.md).

## Quando usar

Intent claro de otimizar / montar / refrescar CV (“otimizar currículo”, “optimize CV”, “gerar master CV”, …).

- Vaga específica → [adapt-cv-to-job.md](adapt-cv-to-job.md) (não este path sozinho).
- LinkedIn → stub local `portfolio/_/optimize-linkedin` (não executar aqui).
- Estudo/empresas → stub local `portfolio/_/study-planning` (não executar aqui).

## Sequência

```
Pipeline A progress:
- [ ] 1. Goals (Soft Gate)     → references/goals-intake.md
- [ ] 2. Append se houver material → references/append-data-to-cv.md
- [ ] 3. Git → experience (por repo) → skill irmã git-commits-to-cv
- [ ] 4. Consolidation         → references/summarize-into-doc.md
```

Pular passo já feito / não aplicável (ex.: inbox vazio e usuário sem material → pular 2; artefactos git já cobertos → pular 3).

### 1 — Goals (Soft Gate)

- Se `output/goals.md` falta: avisar + oferecer [goals-intake.md](goals-intake.md).
- Usuário pode continuar com defaults do glossário.
- Não hard-bloquear o Pipeline A.

### 2 — Append

- Se `output/inbox/` tem `status: pending` **ou** usuário tem CV/docs/notas: seguir [append-data-to-cv.md](append-data-to-cv.md).
- Caso contrário, pular.

### 3 — git-commits-to-cv (Heavy-step)

Para cada repo ainda sem Hybrid Artefact (ou que o usuário queira refrescar):

1. **Pedir** caminho absoluto do Scanned repository (+ company-slug, project-slug, Commit Window).
2. **Confirmar** antes de iniciar o scan (“Posso rodar git-commits-to-cv neste repo?”).
3. Invocar / seguir a skill irmã:

```
.agents/skills/portfolio/git-commits-to-cv/SKILL.md
```

4. **Não** auto-descobrir repos no filesystem.
5. Uma run = um repo (repetir o passo por repo).

### 4 — Consolidation (Heavy-step)

1. Seguir [summarize-into-doc.md](summarize-into-doc.md).
2. **Confirmar** antes de escrever/reescrever `master_cv.md` / `master_cv.en.md`.
3. **Nunca** escrever Portfolio `current_cv.md`.

## Encerrar o Happy Path

Resumir o que rodou, paths tocados, passos pulados, e itens abertos (goals checklist, métricas placeholder). Se pedirem LinkedIn/estudo/empresas → apontar stubs em `portfolio/_/`. Adapt à vaga → [adapt-cv-to-job.md](adapt-cv-to-job.md).
