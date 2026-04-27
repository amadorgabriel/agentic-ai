# 🎯 Spott Team - Cursor Configuration

Configuração de Agents, Skills e Rules para o time de desenvolvimento Spott.

## 📁 Estrutura

```
.cursor/
├── agents/              # Subagentes especializados
│   ├── backend-sr.md    # C# .NET Developer
│   ├── frontend-sr.md   # React/Next.js Developer
│   ├── qa-reviewer.md   # QA Engineer
│   ├── po-product.md    # Product Owner
│   └── tech-lead.md     # Tech Lead (Orquestrador)
│
├── skills/              # Skills reutilizáveis
│   ├── create-pr/       # Criar PRs padronizados
│   ├── grill-me/        # Challenge de requisitos
│   ├── jobs-to-be-done/ # Resumo diário de trabalho
│   └── clickup-sync/    # Sincronizar ClickUp
│
├── rules/               # Regras de workflow
│   └── workflow.md     # Processos do time
│
├── workspace.json      # Configuração do workspace
└── README.md           # Este arquivo
```

## 🤖 Agents

### Como usar
Para usar um agent, simplesmente mencione-o na conversa:

```
@tech-lead preciso revisar esta arquitetura
@backend-sr implementar endpoint de usuários
@frontend-sr criar componente de tabela
@qa-reviewer revisar este PR
@po-product criar PRD para nova feature
```

### Descrição dos Agents

| Agent | Especialidade | Contexto |
|-------|---------------|----------|
| `backend-sr` | C# .NET, APIs, EF Core, RabbitMQ | `spott/` |
| `frontend-sr` | React, Next.js 14, TypeScript, Tailwind | `Spott-cms/` |
| `qa-reviewer` | Testes, Code Review, Segurança | Todos |
| `po-product` | PRDs, ClickUp, Slack, Backlog | Todos |
| `tech-lead` | Orquestração, Arquitetura, PRs | Todos |

## 🛠️ Skills

### Como usar
Para usar uma skill, invoque pelo nome:

```
/jobs-to-be-done
/create-pr
/grill-me sobre [tópico]
/clickup-sync task CU-123456
```

### Skills Disponíveis

| Skill | Descrição | Quando usar |
|-------|-----------|-------------|
| `jobs-to-be-done` | Resumo diário de tasks e PRs | Início do dia |
| `create-pr` | Criar PRs padronizados | Ao terminar feature |
| `grill-me` | Challenge de requisitos | Antes de decisões importantes |
| `clickup-sync` | Sincronizar ClickUp | Durante workflow |

## 📋 Rules

### Workflow do Time
Acesse em `.cursor/rules/workflow.md` para ver:
- Convenções de código
- Processo de desenvolvimento
- Checklists
- Comandos úteis

## 🚀 Workflow Diário Recomendado

### Manhã (09:00)
```
1. Rode: /jobs-to-be-done
2. Revise tasks e PRs pendentes
3. Planeje o dia
```

### Durante o Dia
```
1. Ao pegar task: /clickup-sync task CU-123456
2. Desenvolva com agent apropriado
3. Ao terminar: /create-pr
```

### Final do Dia
```
1. Atualize ClickUp
2. Reporte status
3. Prepare amanhã
```

## 🔗 Integrações

### ClickUp ↔ GitHub
- Branch naming: `feature/CU-123456-descricao`
- Commits: `feat: descricao

CU-123456 #comment progresso`
- PRs: Link da task na descrição

### Slack
- Daily updates: `#dev-updates`
- Bloqueios: `#dev-blockers`
- Releases: `#releases`

## 📚 Documentação Adicional

- [Backend Guidelines](agents/backend-sr.md)
- [Frontend Guidelines](agents/frontend-sr.md)
- [QA Process](agents/qa-reviewer.md)
- [PO Workflow](agents/po-product.md)
- [Tech Lead Guide](agents/tech-lead.md)
- [Team Workflow](rules/workflow.md)

## ⚙️ Configuração

O arquivo `workspace.json` define:
- Pastas do workspace
- Agents disponíveis
- Skills disponíveis
- Contexto de cada agent

---

**Spott Team** 🚀
