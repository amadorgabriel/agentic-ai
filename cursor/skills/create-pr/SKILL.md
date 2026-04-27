---
name: create-pr
description: Cria Pull Requests com template padronizado do time Spott. Use ao finalizar uma feature para gerar descrição estruturada com descrição em bullets, link ClickUp e evidências.
---

# Create PR Skill

## Propósito
Cria Pull Requests com template padronizado do time Spott, incluindo descrição em bullets, link ClickUp e screenshots.

## Quando Usar
- Finalizou uma feature e precisa criar PR
- Quer seguir padrão de descrição do time
- Precisa linkar PR com task do ClickUp

## ⚠️ Flags Anti-Alucinação
- **NEVER** invente números de tasks ClickUp - sempre extraia do branch ou peça ao usuário
- **NEVER** crie screenshots fictícios - só inclua se o usuário fornecer
- **NEVER** invente mudanças que não existem no código - leia o diff antes
- **ALWAYS** verifique o nome da branch para extrair CU-ID
- **ALWAYS** confirme com o usuário antes de criar o PR

## Template de PR

### Estrutura Padrão Spott
```markdown
## Descrição
- [Mudança 1 em português ou inglês conforme contexto]
- [Mudança 2]
- [Mudança 3]

## Task
https://app.clickup.com/t/[CU-ID]

## Evidência
[Se o usuário forneceu screenshots, insira aqui com syntax GitHub]
<img width="1440" height="827" alt="[descrição]" src="[URL]" />
```

### Exemplo Real
```markdown
## Descrição
- Corrige erros de semântica em en-US e pt-BR
- Exibe a tela de detalhes da transação em um side panel

## Task
https://app.clickup.com/t/86ah2qmmx

## Evidência
<img width="1440" height="827" alt="Screenshot 2026-04-24 at 17 02 55" src="https://github.com/user-attachments/assets/287a740f-27ec-4803-9843-cb59703ff3b3" />
<img width="1438" height="827" alt="Screenshot 2026-04-24 at 17 03 02" src="https://github.com/user-attachments/assets/bbcbf016-2f47-4c35-b04b-9d356714ef24" />
```

## Vertical Slice: Workflow de Criação

### Passo 1: Identificar Task
```bash
# Verificar nome da branch atual
git branch --show-current

# Extrair CU-ID do nome da branch (formato: feature/CU-123456-nome)
# Se não encontrar CU-ID, perguntar ao usuário
```
**Flag:** Se branch não seguir padrão `feature/CU-XXXXX`, **PERGUNTE** ao usuário pelo link da task.

### Passo 2: Ler Mudanças
```bash
# Ver diff da branch em relação à main
git diff main...HEAD --stat
git diff main...HEAD --name-only
```
**Flag:** **NUNMA** invente mudanças - leia o diff real do código.

### Passo 3: Gerar Descrição
- Liste mudanças em bullets (máximo 5 items)
- Use linguagem simples e direta
- Foque no que o usuário vê/interage

### Passo 4: Obter Evidências
**Pergunte ao usuário:**
"Você tem screenshots ou evidências para incluir no PR? Cole as imagens aqui."

**Flag:** Se não houver evidências, crie o PR sem seção de evidência.

### Passo 5: Criar PR
```bash
# Push branch se necessário
git push -u origin $(git branch --show-current)

# Criar PR com template
gh pr create \
  --title "feat: [descrição curta]" \
  --body "[CONTEÚDO DO TEMPLATE]" \
  --base main
```

## Convenção de Commits

```
feat: nova funcionalidade
fix: correção de bug
docs: documentação
style: formatação (sem mudança de código)
refactor: refatoração de código
test: adição/correção de testes
chore: tarefas de build, CI, etc
```

**Exemplo:**
```
feat: implementa exportação de relatórios

CU-123456 #comment implementação finalizada
```

## Regras de Ouro
1. **Sempre** use o template Spott (Descrição/Task/Evidência)
2. **Sempre** inclua link ClickUp válido
3. **Nunca** invente screenshots ou evidências
4. **Nunca** crie descrições sem ler o diff real
5. **Sempre** confirme com usuário antes de executar `gh pr create`
