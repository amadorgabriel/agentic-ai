---
name: jobs-to-be-done
description: Gera resumo diário de trabalho com tasks do ClickUp (done, to-do, blocked), PRs abertos no GitHub e status do time. Use proativamente no início do dia para planejamento.
---

# Jobs-to-be-done Skill

## Propósito
Gera um resumo completo do dia de trabalho: tasks concluídas, pendentes, bloqueadas, PRs abertos e status do time.

## Quando Usar
- Começando o dia de trabalho
- Precisa de visão geral do que fazer
- Quer ver PRs abertos para revisar
- Precisa reportar status para stakeholders

## ⚠️ Flags Anti-Alucinação
- **NEVER** invente tasks que não existem no ClickUp - execute os comandos reais
- **NEVER** invente PRs - sempre use `gh pr list` para obter dados reais
- **NEVER** assuma status de CI sem verificar `gh run list`
- **ALWAYS** execute comandos reais de CLI antes de reportar
- **ALWAYS** quando não conseguir executar comando, informe: "[Dado não disponível - verificar manualmente]"

## Output Esperado

```
📅 Jobs to be Done - [Data]

═══════════════════════════════════════════
✅ CONCLUÍDO (Últimas 24h)
═══════════════════════════════════════════
• [Task 1] - [Status] - [Link ClickUp]
• [Task 2] - [Status] - [Link ClickUp]

═══════════════════════════════════════════
🎯 PARA FAZER HOJE
═══════════════════════════════════════════
[Prioridade Alta]
• [Task 1] - [Tempo estimado] - [Link]
  └─ [Breve descrição]

[Prioridade Média]
• [Task 2] - [Link]

═══════════════════════════════════════════
🚧 BLOQUEADOS
═══════════════════════════════════════════
• [Task 1]
  └─ Bloqueio: [Motivo]
  └─ Ação: [Próximo passo]
  └─ Responsável: [Quem deve agir]

═══════════════════════════════════════════
📥 PULL REQUESTS ABERTOS
═══════════════════════════════════════════
[Para Revisar]
• #XXX: [Título] por @author
  └─ Status CI: [✅/❌/⏳]
  └─ Aberto há: [X dias]

[Meus PRs]
• #XXX: [Título]
  └─ Reviews: [X/X aprovados]
  └─ Status: [Aguardando/Merge pronto]

═══════════════════════════════════════════
🎯 FOCO DO DIA
═══════════════════════════════════════════
1. [Task prioridade 1]
2. [Task prioridade 2]
3. [Code reviews pendentes]
```

## Vertical Slice: Coleta de Dados

### Passo 1: Tasks Concluídas
Execute:
```bash
clickup task list --assignee @me --status "Complete" --updated-last 24h
```
**Fallback:** Se comando falhar, exiba: "⚠️ Não foi possível obter tasks concluídas - verificar manualmente no ClickUp"

### Passo 2: Tasks Pendentes
Execute:
```bash
clickup task list --assignee @me --due-date today
clickup task list --assignee @me --status "In Progress"
```
**Fallback:** Se comando falhar, pergunte ao usuário: "Quais são suas principais tasks para hoje?"

### Passo 3: Tasks Bloqueadas
Execute:
```bash
clickup task list --assignee @me --status "Blocked"
```
**Flag:** Se não houver comando de blocked, procure tasks com tag "blocked" ou status personalizado.

### Passo 4: PRs Abertos
Execute:
```bash
gh pr list --state open --limit 15
gh pr list --author "@me" --state open
```
**Fallback:** Se `gh` não estiver disponível, exiba: "📥 PRs: [Verificar manualmente em github.com]"

### Passo 5: Status CI
Execute:
```bash
gh run list --limit 5 --workflow "CI"
```
**Flag:** Só reporte status de CI se conseguir executar o comando real.

## Personalização por Projeto

### Frontend (Spott-cms)
```bash
clickup task list --list "Frontend" --status "In Progress"
```

### Backend (spott)
```bash
clickup task list --list "Backend" --status "In Progress"
```

### Admin (Spott.Admin)
```bash
clickup task list --list "Admin" --status "In Progress"
```

## Workflow Diário

### Manhã (09:00)
1. Execute `/jobs-to-be-done`
2. Aguarde execução dos comandos reais
3. Revise output com dados reais
4. Copie resumo para Slack se desejado

### Durante o Dia
- Atualize progresso no ClickUp manualmente
- Execute novamente se precisar de status atualizado

### Final do Dia
- Revise o que foi concluído
- Prepare prioridades para amanhã

## Regras de Ouro
1. **SEMPRE** execute comandos reais antes de reportar
2. **NUNCA** invente dados de tasks ou PRs
3. **SEMPRE** informe quando um dado não pôde ser obtido
4. **SEMPRE** priorize code reviews junto com desenvolvimento
5. **SEMPRE** mantenha formato consistente de output
