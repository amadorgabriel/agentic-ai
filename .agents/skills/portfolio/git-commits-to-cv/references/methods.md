# Métodos — XYZ e STAR (PT-BR, ATS)

Orientação para escrever o **Hybrid Artefact**. Alinhado a [agentic-career/context/cv-from-commits/CONTEXT.md](../../agentic-career/context/cv-from-commits/CONTEXT.md). Não inventar trabalho nem métricas.

## XYZ (camada CV)

Fórmula Google XYZ: **conquistou X medido por Y fazendo Z**.

| Parte | Significado | Exemplo (PT-BR) |
| --- | --- | --- |
| **X** | Resultado / impacto de negócio ou produto | Reduzi tempo de carregamento da listagem |
| **Y** | Medida verificável | de 4,2s para 1,1s (LCP) |
| **Z** | Como (tecnologia / abordagem evidenciada nos commits) | via virtualização e cache TanStack Query |

### Regras

1. Uma linha por bullet; acionável e escaneável por ATS (verbos fortes no início ou impacto claro).
2. Preferir evidência em commits/PRs/docs do repo; se Y faltar → `[MÉTRICA A CONFIRMAR]`.
3. **Nunca** inventar percentuais, latência, throughput, headcount ou receita.
4. Produzir **5–8** bullets de topo (clusters), não um por commit.
5. Viés de papel (default Fullstack Pleno): priorizar API, dados, auth, cloud e FE **quando constarem** no histórico — sem fabricar ownership.
6. Evitar jargão interno opaco; preferir termos reconhecíveis (API, migração, CI/CD, Design System).

### Bom vs ruim

**Bom:**
> Acelerei o checkout mobile em `[MÉTRICA A CONFIRMAR]` ao extrair o fluxo de pagamento para um módulo isolado com TypeScript e testes de integração.

**Ruim (métrica inventada):**
> Melhorei a performance em 47% refatorando o checkout.

**Ruim (changelog):**
> Commit: fix button; Commit: update styles; Commit: merge main.

**Ruim (STAR no CV):**
> Em uma situação em que o time enfrentava… (parágrafo longo) — isso vai na seção STAR, não no bullet XYZ.

### Viés por Target Role Bias

| Modo | Priorizar na frase | Ainda assim |
| --- | --- | --- |
| Fullstack Engineer Pleno (default) | ponta a ponta: API + dados + auth + cloud + FE | só o que os commits mostram |
| Frontend Pleno | UI, a11y, Design System, perf web, estado cliente | não inventar backend |
| neutral | impacto técnico sem forçar full-stack | idem |

## STAR (camada entrevista)

Uma nota STAR por conquista relevante (pareada ao bullet XYZ). Não consolida em `current_cv.md` por padrão.

| Letra | Pergunta | Dica |
| --- | --- | --- |
| **S** Situação | Qual era o contexto do produto/time? | 1–3 frases; fato, não drama |
| **T** Tarefa | Qual era a responsabilidade / objetivo? | Escopo pessoal vs time — seja honesto |
| **A** Ação | O que *você* fez? | Ligar a temas/hashes de commits |
| **R** Resultado | O que mudou? | Métrica real ou `[MÉTRICA A CONFIRMAR]` |

### Regras STAR

1. PT-BR; conciso o bastante para ensaiar em entrevista (~30–90s falados).
2. Ação deve ser rastreável a clusters de commits (citar hashes na seção de evidência).
3. Resultado sem evidência → placeholder; listar no Validation Checklist.
4. Em **Smart Merge**: preservar STAR confirmadas/editadas pelo usuário; só reescrever se nova evidência contradisser ou o usuário pedir.

## Métricas e checklist

1. Procurar Y em: mensagens de commit, PRs, CHANGELOG, docs do repo, comentários de review (se acessíveis).
2. Se não achar: escrever XYZ com `[MÉTRICA A CONFIRMAR]` e adicionar item no checklist.
3. Perguntar interativamente **somente** para bullets de topo/alto valor sem Y.
4. Bullets mais fracos: placeholder ou omitir Y fabricado — sem interromper o fluxo.
5. Números que o usuário confirmar na conversa: gravar no artefacto e marcar como confirmados (para Smart Merge preservar).

## ATS (rápido)

- Preferir substantivos e verbos concretos (implementei, migrei, reduzi, estabilizei).
- Evitar markdown extravagante dentro do bullet (sem bold excessivo; uma linha limpa).
- Manter keywords técnicas reais do projeto (React, .NET, OCPP, etc.) quando evidenciadas.
- Não encher de soft-skills genéricas (“trabalhei bem em equipe”) sem evidência de entrega.
