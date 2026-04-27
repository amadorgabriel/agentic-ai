---
name: to-issues
description: Quebra um plano, spec ou PRD em issues GitHub independentes usando fatias verticais tracer bullet. Use quando o usuário quer converter um plano em issues, criar tickets de implementação ou dividir trabalho em issues.
---

# To Issues

Quebre um plano em issues GitHub independentes usando fatias verticais (tracer bullets).

## Processo

### 1. Coletar Contexto

Trabalhe com o que já está no contexto da conversa. Se o usuário passar um número ou URL de issue GitHub como argumento, busque com `gh issue view <number>` (com comentários).

### 2. Explorar Codebase (opcional)

Se você ainda não explorou o codebase, faça-o para entender o estado atual do código.

### 3. Rascunhar Fatias Verticais

Quebre o plano em issues **tracer bullet**. Cada issue é uma fatia vertical fina que corta TODAS as camadas de integração end-to-end, NÃO uma fatia horizontal de uma camada.

As fatias podem ser 'HITL' ou 'AFK'. Fatias HITL requerem interação humana, como decisão arquitetural ou design review. Fatias AFK podem ser implementadas e mergeadas sem interação humana. Prefira AFK sobre HITL quando possível.

<vertical-slice-rules>
- Cada fatia entrega um caminho completo mas estreito através de todas as camadas (schema, API, UI, tests)
- Uma fatia completa é demonstrável ou verificável por si só
- Prefira muitas fatias finas sobre poucas grossas
</vertical-slice-rules>

### 4. Questionar o Usuário

Apresente a quebra proposta como uma lista numerada. Para cada fatia, mostre:

- **Título**: nome descritivo curto
- **Tipo**: HITL / AFK
- **Bloqueado por**: quais outras fatias (se houver) devem completar primeiro
- **User stories cobertas**: quais user stories isto endereça (se o material fonte tiver)

Pergunte ao usuário:

- A granularidade parece certa? (muito grosso / muito fino)
- Os relacionamentos de dependência estão corretos?
- Alguma fatia deveria ser mergeada ou dividida?
- As fatias corretas estão marcadas como HITL e AFK?

Itere até o usuário aprovar a quebra.

### 5. Criar as GitHub Issues

Para cada fatia aprovada, crie uma issue GitHub usando `gh issue create`. Use o template abaixo para o corpo da issue.

Crie issues na ordem de dependência (bloqueadores primeiro) para poder referenciar números reais de issues no campo "Blocked by".

<issue-template>
## Parent

#<parent-issue-number> (se a fonte era uma issue GitHub, senão omita esta seção)

## O que construir

Uma descrição concisa desta fatia vertical. Descreva o comportamento end-to-end, não implementação camada-por-camada.

## Critérios de aceitação

- [ ] Critério 1
- [ ] Critério 2
- [ ] Critério 3

## Bloqueado por

- Bloqueado por #<issue-number> (se houver)

Ou "Nenhum - pode começar imediatamente" se não houver bloqueadores.

</issue-template>

NÃO feche ou modifique nenhuma issue pai.
