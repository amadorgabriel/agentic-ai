---
name: triage-issue
description: Triagem e análise de issues/bugs para classificação, priorização e atribuição. Use quando o usuário quer analisar um bug, classificar severidade, ou determinar próximos passos para uma issue.
---

# Triage Issue

Analise e classifique issues/bugs sistematicamente para determinar severidade, prioridade e próximos passos.

## Quando Usar

- Novo bug reportado precisa ser analisado
- Issue chegou sem informações suficientes
- Precisa determinar severidade e prioridade
- Verificar se é duplicado de issue existente
- Determinar se precisa de mais informações

## ⚠️ Flags Anti-Alucinação
- **NEVER** assuma severidade sem analisar o impacto real
- **NEVER** marque como duplicado sem verificar issues existentes
- **NEVER** atribua sem confirmar com o usuário
- **ALWAYS** verifique se há logs, screenshots ou passos de reprodução
- **ALWAYS** confirme severidade antes de priorizar

## Workflow de Triagem

### 1. Coletar Informações

Verifique se a issue contém:

- [ ] **Título claro** - descreve o problema em uma linha
- [ ] **Descrição do problema** - o que está acontecendo
- [ ] **Passos para reproduzir** - como reproduzir o bug
- [ ] **Comportamento esperado** - o que deveria acontecer
- [ ] **Comportamento atual** - o que está acontecendo de errado
- [ ] **Screenshots/vídeos** - evidências visuais
- [ ] **Logs/erros** - mensagens de erro ou stack traces
- [ ] **Ambiente** - browser, OS, versão do app
- [ ] **Contexto** - quando começou, quem está afetado

### 2. Verificar Duplicados

Busque issues existentes similares:

```bash
# Listar issues abertas
gh issue list --state open --limit 20

# Buscar por palavras-chave do problema
gh issue list --search "[termo-chave]"
```

**Se encontrar duplicado:**
- Comente na issue original mencionando o novo report
- Feche a duplicada com referência: "Duplicado de #XXX"

### 3. Classificar Severidade

| Severidade | Critérios | SLA |
|-----------|-----------|-----|
| **P0 - Critical** | Sistema inoperante, dados corrompidos, segurança comprometida | 4h |
| **P1 - High** | Funcionalidade core quebrada, workaround difícil | 24h |
| **P2 - Medium** | Funcionalidade não-core afetada, workaround disponível | 1 semana |
| **P3 - Low** | Cosmetic, enhancement, edge case | Next sprint |

**Perguntas para determinar severidade:**
- Quantos usuários estão afetados?
- É possível contornar o problema?
- Há impacto em dados/receita/segurança?
- A funcionalidade é crítica para o negócio?

### 4. Determinar Tipo

- **Bug** - comportamento não esperado
- **Feature** - nova funcionalidade
- **Task** - trabalho técnico (refactor, config)
- **Enhancement** - melhoria em funcionalidade existente
- **Documentation** - docs, comentários, README

### 5. Identificar Área/Time

Baseado no contexto, determine:

- **Frontend** - UI, componentes, formulários
- **Backend** - API, banco de dados, lógica de negócio
- **Mobile** - app iOS/Android
- **DevOps** - CI/CD, deploy, infra
- **Design** - UX, mockups, protótipos

### 6. Avaliar Informações Faltantes

Se faltam informações críticas, solicite:

> **Informações necessárias para prosseguir:**
> - [ ] Passos exatos para reproduzir
> - [ ] Screenshot ou vídeo do problema
> - [ ] Logs de erro (console, network, server)
> - [ ] Ambiente onde ocorreu (browser/OS/versão)
> - [ ] Dados de entrada que causaram o problema

Marque a issue com label: `needs-info`

### 7. Próximos Passos Recomendados

Baseado na triagem, determine ação:

| Situação | Ação |
|----------|------|
| Info completa + Severidade clara | Atribuir ao time/dev apropriado |
| Falta informação crítica | Solicitar mais info, label `needs-info` |
| Duplicado | Fechar com referência |
| Não é bug (comportamento esperado) | Explicar e fechar |
| Precisa de discussão técnica | Marcar com label `needs-discussion` |
| Muito grande | Quebrar em issues menores |

## Checklist de Triagem

```markdown
## Triagem de Issue #XXX

### Informações Coletadas
- [ ] Título descritivo
- [ ] Descrição clara do problema
- [ ] Passos de reprodução
- [ ] Comportamento esperado vs atual
- [ ] Evidências (screenshots/logs)
- [ ] Ambiente identificado

### Classificação
- **Severidade:** [P0/P1/P2/P3]
- **Tipo:** [Bug/Feature/Task/Enhancement]
- **Área:** [Frontend/Backend/Mobile/DevOps/Design]
- **Duplicado:** [Sim #XXX / Não]

### Decisão
- [ ] Pronto para desenvolvimento
- [ ] Precisa de mais informações
- [ ] Precisa de discussão técnica
- [ ] Não é bug

### Próximos Passos
1. [Ação específica]
2. [Responsável]
3. [Prazo/SLA]
```

## Comandos Úteis

```bash
# Ver issue específica
gh issue view <number>

# Listar issues por label
gh issue list --label "bug"
gh issue list --label "needs-info"

# Adicionar labels
gh issue edit <number> --add-label "P1,frontend,needs-info"

# Comentar na issue
gh issue comment <number> --body "[mensagem]"

# Fechar issue
gh issue close <number> --comment "Duplicado de #XXX"
```

## Exemplo de Comentário de Triagem

```markdown
## 🏷️ Triagem Realizada

**Severidade:** P2 - Medium
**Tipo:** Bug
**Área:** Frontend

**Análise:**
O problema ocorre na tela de cupons quando o usuário tenta aplicar um código inválido. Não causa crash, mas exibe mensagem de erro genérica em vez de específica.

**Decisão:**
✅ Issue pronta para desenvolvimento

**Próximos Passos:**
1. Atribuir ao time Frontend
2. Estimar esforço
3. Incluir na próxima sprint

**Notas:**
- Não é duplicado (verificamos #123, #145)
- Impacto estimado: ~50 usuários/dia
- Workaround: recarregar página e tentar novo código
```

## Regras de Ouro
1. **SEMPRE** verifique duplicados antes de criar nova issue
2. **SEMPRE** classifique severidade baseada em impacto real, não sensação
3. **NUNCA** atribua sem confirmar disponibilidade do dev/time
4. **SEMPRE** comunique decisões de triagem de forma clara
5. **SEMPRE** mantenha labels atualizados refletindo estado atual
