# agentic-ai

Minhas configurações de agents, skills e rules para desenvolvimento.

### Estrutura

```
.cursor/
├── agents/                 # Subagentes especializados
│   ├── backend-sr.md       # C# .NET Developer
│   ├── frontend-sr.md      # React/Next.js Developer
│   ├── qa-reviewer.md      # QA Engineer
│   ├── po-product.md       # Product Owner
│   └── tech-lead.md        # Tech Lead (Orquestrador)
├── skills/                 # Skills reutilizáveis
├── rules/                  # Regras de workflow
│   └── workflow.md        # Processos do time
├── workspace.json         # Configuração do workspace
└── README.md              # Este arquivo
```

### Descrição dos Agents

| Agent | Especialidade | Contexto |
|-------|---------------|----------|
| `backend-sr` | C# .NET, APIs, EF Core, RabbitMQ | `server/` |
| `frontend-sr` | React, Next.js 14, TypeScript, Tailwind | `client/` |
| `qa-reviewer` | Testes, Code Review, Segurança | Todos |
| `po-product` | PRDs, ClickUp, Slack, Backlog | Todos |
| `tech-lead` | Orquestração, Arquitetura, PRs | Todos |


### Skills Principais

| Skill | Descrição | Quando usar |
|-------|-----------|-------------|
| `jobs-to-be-done` | Resumo diário de tasks e PRs | Início do dia |
| `create-pr` | Criar PRs padronizados | Ao terminar feature |
| `clickup-sync` | Sincronizar ClickUp com GitHub | Durante workflow |
| `design-an-interface` | Gerar múltiplos designs de interface | Projetar APIs ou componentes |
| `grill-me` | Challenge de requisitos | Antes de decisões importantes |
| `improve-front-arch` | Padronizar módulo ao padrão coupons | Refatorar/criar módulos frontend |
| `to-vertical-slices` | Quebrar plano em issues GitHub | Dividir trabalho em tickets |
| `triage-issue` | Triagem e classificação de bugs | Analisar novas issues |
| `write-prd` | Criar novos skills para o time | Desenvolver novas capacidades |

<br />

<div style="text-align: center;">
  Feito com 🤖💛
</div>

