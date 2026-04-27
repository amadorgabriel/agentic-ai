---
description: Regras de workflow do time Spott - como usar agents, skills e processos de desenvolvimento
---

# Regras de Workflow - Spott Team

## Visão Geral
Este documento define como usar os agents, skills e processos do time Spott de forma eficiente.

## Estrutura do Time

```
Spott Team
├── Tech Lead (Orquestrador)
├── Backend SR (C# .NET)
├── Frontend SR (React/Next.js)
├── QA Reviewer (Qualidade)
└── PO Product (Negócio)
```

## Quando Usar Cada Agent

### `/tech-lead`
- **Use quando:** Precisa coordenar o time, revisar arquitetura complexa, gerenciar PRs
- **Comandos comuns:**
  - `/jobs-to-be-done` - Resumo diário
  - `/create-pr` - Criar PRs
  - `/grill-me` - Challenge arquitetural

### `/backend-sr`
- **Use quando:** Trabalhando no projeto `spott` (C# .NET)
- **Comandos comuns:**
  - Desenvolver APIs
  - Criar lógica de negócio
  - Modelar banco de dados

### `/frontend-sr`
- **Use quando:** Trabalhando no projeto `Spott-cms` (React/Next.js)
- **Comandos comuns:**
  - Desenvolver UI
  - Integrar com APIs
  - Criar componentes

### `/qa-reviewer`
- **Use quando:** Precisa revisar código, validar qualidade, sugerir testes
- **Comandos comuns:**
  - Revisar PRs
  - Sugerir cenários de teste
  - Validar acceptance criteria

### `/po-product`
- **Use quando:** Precisa criar especificações, refinar backlog, comunicar stakeholders
- **Comandos comuns:**
  - `/grill-me` - Refinar requisitos
  - Criar PRDs
  - Sincronizar ClickUp

## Skills Disponíveis

### `/jobs-to-be-done`
**Uso:** Início do dia de trabalho
```
/jobs-to-be-done

Output esperado:
- Tasks concluídas ontem
- Tasks para hoje
- PRs abertos
- Bloqueios
- Foco do dia
```

### `/create-pr`
**Uso:** Ao finalizar uma feature
```
/create-pr

Workflow:
1. Prepara: branch, commits
2. Gera descrição padronizada
3. Cria PR no GitHub
4. Linka com ClickUp
5. Atualiza status
```

### `/grill-me`
**Uso:** Antes de grandes decisões ou quando precisa de challenge
```
/grill-me sobre [tópico]

Exemplos:
- /grill-me sobre arquitetura de microserviços
- /grill-me sobre plano de implementação
- /grill-me sobre design de API
```

### `/clickup-sync`
**Uso:** Sincronizar tasks com código
```
/clickup-sync

Funções:
- Criar branch a partir de task
- Linkar PR com task
- Atualizar status
- Notificar Slack
```

## Workflow Diário Recomendado

### Manhã (09:00)
1. **Abra o Cursor** no workspace Spott
2. **Rode:** `/jobs-to-be-done`
3. **Revise:**
   - Tasks para o dia
   - PRs pendentes de review
   - Bloqueios do time
4. **Comunique:** Status no Slack

### Durante o Dia
1. **Ao pegar uma task:**
   ```
   /clickup-sync task CU-123456
   → Cria branch
   → Atualiza status para "In Progress"
   ```

2. **Ao desenvolver:**
   - Siga padrões do agent (backend-sr ou frontend-sr)
   - Commits com conventional commits
   - Referencie CU-ID nos commits

3. **Ao terminar:**
   ```
   /create-pr
   → Gera descrição
   → Cria PR
   → Linka com ClickUp
   → Atualiza status para "Code Review"
   ```

### End of Day (17:00)
1. **Atualize:** Status de tasks no ClickUp
2. **Reporte:** Bloqueios encontrados
3. **Prepare:** Prioridades para amanhã

## Convenções de Código

### Commits (Conventional Commits)
```
tipo(escopo): descrição

[corpo opcional]

[footer com referências]
```

**Tipos:**
- `feat:` nova funcionalidade
- `fix:` correção de bug
- `docs:` documentação
- `style:` formatação
- `refactor:` refatoração
- `test:` testes
- `chore:` tarefas de build

**Exemplos:**
```
feat(auth): adiciona login com Google

fix(api): corrige validação de token

CU-123456 #comment implementação finalizada
```

### Branches
```
feature/CU-123456-descricao-curta
bugfix/CU-123457-correcao-do-bug
hotfix/CU-123458-correcao-urgente
refactor/CU-123459-melhoria-codigo
```

### PRs
```markdown
## 📋 Descrição
[O que foi feito]

## 🔗 ClickUp
- Task: https://app.clickup.com/t/CU-123456

## 🧪 Como Testar
1. [Passos]

## ✅ Checklist
- [ ] Testes passam
- [ ] Código revisado
- [ ] Documentação atualizada
```

## Integrações

### ClickUp ↔ GitHub
- ID da task sempre na branch: `feature/CU-123456-nome`
- ID da task em commits importantes
- Link da task na descrição do PR

### GitHub → Slack
- PRs criados: notificar `#dev-updates`
- PRs merged: notificar `#releases`
- Builds falhando: notificar `#dev-alerts`

### ClickUp → Slack
- Tasks bloqueadas: `#dev-blockers`
- Releases completados: `#releases`
- Daily status: `#dev-updates`

## Comandos Úteis

### Git
```bash
# Status geral
git status

# Criar branch
git checkout -b feature/CU-123456-nome

# Commit
git commit -m "feat: descrição

CU-123456 #comment progresso"

# Push
git push -u origin feature/CU-123456-nome
```

### GitHub CLI
```bash
# Listar PRs
gh pr list --state open

# Revisar PR
gh pr checkout <number>
gh pr diff <number>
gh pr review <number> --approve

# Criar PR
gh pr create --template
```

### ClickUp CLI
```bash
# Minhas tasks
clickup task list --assignee @me

# Atualizar status
clickup task update CU-123456 --status "Done"

# Comentar
clickup task comment CU-123456 "Mensagem"
```

## Checklists

### Início de Sprint
- [ ] Backlog refinado
- [ ] Tasks estimadas
- [ ] Responsáveis atribuídos
- [ ] Dependências identificadas

### Antes de Commit
- [ ] Código testado localmente
- [ ] Lint passando
- [ ] Sem console.logs/debuggers
- [ ] Commits seguem convenção

### Antes de PR
- [ ] Branch atualizada com main
- [ ] Conflitos resolvidos
- [ ] Testes passando
- [ ] Descrição preenchida
- [ ] Link com ClickUp

### Code Review
- [ ] Código entendido
- [ ] Padrões seguidos
- [ ] Testes cobrem mudanças
- [ ] Sem problemas de segurança
- [ ] Performance aceitável

## Troubleshooting

### "Agent não encontrado"
Verifique se o arquivo `.cursor/agents/[nome].md` existe e tem frontmatter válido.

### "Skill não funciona"
Verifique se o arquivo `.cursor/skills/[nome]/SKILL.md` existe.

### PR não linka com ClickUp
- Confirme se a branch segue o padrão `feature/CU-XXXXX`
- Verifique se o ID está correto
- Adicione link manual na descrição do PR

## Contato e Suporte

- **Dúvidas técnicas:** @tech-lead
- **Dúvidas de negócio:** @po-product
- **Problemas de qualidade:** @qa-reviewer
