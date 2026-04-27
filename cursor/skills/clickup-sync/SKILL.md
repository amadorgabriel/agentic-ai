---
name: clickup-sync
description: Sincroniza tarefas do ClickUp com GitHub e código. Use para criar branches a partir de tasks, linkar PRs com tasks, atualizar status automaticamente.
---

# ClickUp Sync Skill

## Propósito
Integra ClickUp com workflow de desenvolvimento: cria branches a partir de tasks, linka PRs, atualiza status.

## Quando Usar
- Começar a trabalhar em uma task
- Criar branch a partir de task do ClickUp
- Linkar PR com task
- Atualizar status após deploy

## ⚠️ Flags Anti-Alucinação
- **NEVER** invente IDs de tasks - sempre use IDs reais fornecidos ou do ClickUp
- **NEVER** crie branches sem confirmar o formato com o usuário
- **NEVER** assuma qual status usar - pergunte ou use mapeamento definido
- **ALWAYS** extraia CU-ID de URLs ou nomes de branch reais
- **ALWAYS** confirme ações destrutivas (como atualizar status) antes de executar

## Estrutura de Integração

### Mapeamento de Status
```
Desenvolvimento  → "In Progress"
Code Review      → "Code Review" ou "Review"
Testes/QA        → "QA" ou "Testing"
Deploy Staging   → "Staging"
Concluído        → "Done" ou "Complete"
Bloqueado        → "Blocked"
```

## Vertical Slice: Workflows

### Workflow 1: Iniciar Task

#### Passo 1: Obter Task
**Verbos:**
```bash
# Opção A: Listar tasks disponíveis
clickup task list --assignee @me --status "not_started"

# Opção B: Se usuário informou URL
# Extraia CU-ID da URL: https://app.clickup.com/t/86ah2qmmx
# CU-ID = 86ah2qmmx

# Opção C: Se usuário informou ID parcial
clickup task get CU-86ah2qmmx
```

**Flag:** Se não conseguir identificar task, **PERGUNTE:** "Qual o link ou ID da task no ClickUp?"

#### Passo 2: Criar Branch
```bash
# Formato padrão: feature/CU-{id}-{nome-simplificado}
# Exemplo: feature/CU-86ah2qmmx-correcao-semantica

# Obter nome da task para slug
clickup task get [CU-ID] --format "{{name}}"

# Criar branch
git checkout -b feature/CU-[ID]-[slug-da-task]
```

**Flag:** **SEMPRE** confirme com usuário:
> "Vou criar a branch `feature/CU-86ah2qmmx-correcao-semantica`. Confirma?"

#### Passo 3: Atualizar Status
```bash
# Atualizar para "In Progress"
clickup task update [CU-ID] --status "In Progress"
```

#### Passo 4: Comentar
```bash
# Adicionar comentário com link do branch
clickup task comment [CU-ID] "Branch criada: feature/CU-[ID]-[nome]"
```

---

### Workflow 2: Linkar PR com Task

#### Passo 1: Extrair CU-ID
```bash
# Da branch atual
git branch --show-current
# Extrai: feature/CU-86ah2qmmx-nome → CU-86ah2qmmx
```

**Flag:** Se branch não seguir padrão, **PERGUNTE:** "Qual o link da task no ClickUp?"

#### Passo 2: Criar PR com Template
Ver `/create-pr` skill para template de PR.

**Incluir na descrição:**
```markdown
## Task
https://app.clickup.com/t/[CU-ID]
```

#### Passo 3: Atualizar Status
```bash
clickup task update [CU-ID] --status "Code Review"
clickup task comment [CU-ID] "PR criado: [URL do PR]"
```

---

### Workflow 3: Finalizar Task

#### Passo 1: Após Merge
```bash
clickup task update [CU-ID] --status "Done"
clickup task comment [CU-ID] "✅ Mergeado para main em [SHA do commit]"
```

#### Passo 2: Após Deploy
```bash
clickup task update [CU-ID] --status "Closed"
clickup task comment [CU-ID] "🚀 Deployado em produção em [data]"
```

---

## Comandos de Referência

### Tasks
```bash
# Listar minhas tasks
clickup task list --assignee @me

# Ver detalhes
clickup task get [CU-ID]

# Atualizar status
clickup task update [CU-ID] --status "[STATUS]"

# Comentar
clickup task comment [CU-ID] "[MENSAGEM]"

# Mover para sprint
clickup task update [CU-ID] --list "Sprint [N]"
```

### Git
```bash
# Criar branch a partir de task
git checkout -b feature/CU-[ID]-[nome]

# Commit com referência
git commit -m "feat: descrição

CU-[ID] #comment progresso"

# Push
git push -u origin feature/CU-[ID]-[nome]
```

## Regras de Ouro
1. **SEMPRE** confirme ações antes de executar
2. **NUNCA** atualize status sem confirmação do usuário
3. **SEMPRE** use formato `feature/CU-[ID]-[nome]` para branches
4. **NUNCA** invente IDs de tasks
5. **SEMPRE** comente links úteis (branch, PR) na task

## Troubleshooting

### "Task não encontrada"
```bash
# Buscar por nome
clickup task list --search "[termo]"

# Listar todas do usuário
clickup task list --assignee @me --limit 50
```

### "Branch já existe"
```bash
# Usar nome alternativo
git checkout -b feature/CU-[ID]-[nome]-v2
```

### "Não tenho CLI do ClickUp"
Execute atualizações manualmente:
1. Abra a task no browser
2. Atualize status manualmente
3. Adicione comentário manualmente
