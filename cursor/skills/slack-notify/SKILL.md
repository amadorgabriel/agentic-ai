---
name: slack-notify
description: Envia somente notificação de novo PR no canal devs-spott usando o alias slack-cli.
---

# Slack Notify Skill

## Propósito
Integra Slack ao workflow de desenvolvimento do Spott para um único caso: notificar novo PR no canal devs-spott usando slack-cli.

## Quando Usar
- Notificar time sobre novo PR criado

## ⚠️ Flags Anti-Alucinação
- **NEVER** invente canais - use somente `devs-spott`
- **ALWAYS** confirme menções antes de enviar
- **ALWAYS** use o formato padronizado para notificações de PR
- **NEVER** envie mensagens fora do canal `devs-spott`
- **ALWAYS** use o comando `slack-cli` (não use `slackcli.exe`)

## Pré-requisitos

### Instalação slack-cli
```powershell
# Windows
$url = "https://downloads.slack-edge.com/slack-cli/bin/windows/slack_cli.zip"
Invoke-WebRequest -Uri $url -OutFile "$env:TEMP\slack_cli.zip"
Expand-Archive -Path "$env:TEMP\slack_cli.zip" -DestinationPath "$env:LOCALAPPDATA\slack-cli"
```

### Autenticação
```bash
# Login único necessário
slack-cli login
# Seguir fluxo de autenticação no browser
```

## Estrutura de Integração

### Canais Padrão
```
devs-spott    → Único canal permitido para esta skill
```

### Mapeamento de Usuários (IDs Slack)
```
Leonardo Victor → @Leonardo Victor
Gabriel Guimarães → @Gabriel Guimarães
Raphael → @Raphael
Danilo Santos → @Danilo Santos
```

## Vertical Slice: Workflows

### Workflow 1: Notificar Novo PR

#### Passo 1: Identificar Contexto
**Verbos:**
```bash
# Obter branch atual
git branch --show-current
# Extrai: feature/CU-86ah2d7p3-faulted-status → CU-86ah2d7p3

# Obter URL do PR (se já criado)
gh pr view --json url --jq '.url'
```

#### Passo 2: Construir Mensagem
**Template padrão:**
```
PR: {CMS para front or Spott para back} | {repository_name} | {pr_name}
{link}
@Danilo Santos @Leonardo Victor @Raphael @Gabriel Guimarães
```

**Exemplo:**
```
PR: CMS para front | Spott-eco/Spott-cms | [BUG] Adicionar status de Faulted nos plugues do carregador
https://github.com/Spott-eco/Spott-cms/pull/622
@Danilo Santos @Leonardo Victor @Raphael @Gabriel Guimarães
```

#### Passo 3: Enviar Mensagem
```bash
slack-cli chat post \
  --channel "devs-spott" \
  --message "PR: CMS para front | Spott-eco/Spott-cms | [BUG] Adicionar status de Faulted nos plugues do carregador
https://github.com/Spott-eco/Spott-cms/pull/622
@Danilo Santos @Leonardo Victor @Raphael @Gabriel Guimarães"
```

## Comandos de Referência

### slack-cli
```bash
# Enviar mensagem
slack-cli chat post --channel "devs-spott" --message "[MENSAGEM]"

# Listar canais
slack-cli channel list

# Verificar status
slack-cli status

# Logout
slack-cli logout
```

### Menções
```
<@username>     → Menção usuário específico
<!here>          → Notifica usuários online
<!channel>       → Notifica todos no canal
<!everyone>      → Notifica todos (use com cautela)
```

## Regras de Ouro
1. **SEMPRE** use template padronizado para PRs
2. **SEMPRE** envie somente no canal `devs-spott`
3. **SEMPRE** use o alias `slack-cli`
4. **NUNCA** envie credenciais ou dados sensíveis
5. **SEMPRE** confirme menções de pessoas

## Troubleshooting

### "Não autenticado"
```bash
slack-cli login
# Autentique no browser
```

### "Canal não encontrado"
```bash
# Listar canais disponíveis
slack-cli channel list

# Esta skill só permite o canal devs-spott
slack-cli chat post --channel "devs-spott" --message "test"
```

### "Mensagem não enviada"
- Verificar permissões no canal
- Verificar limite de caracteres (4000)
- Verificar formatação markdown

### "slack-cli não encontrado"
```powershell
# Verificar instalação
Test-Path "$env:LOCALAPPDATA\slack-cli\bin\slack-cli.exe"

# Adicionar ao PATH (temporário)
$env:PATH += ";$env:LOCALAPPDATA\slack-cli\bin"
```
