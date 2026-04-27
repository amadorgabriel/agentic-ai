---
name: write-a-skill
description: Cria novos skills de agent com estrutura adequada, revelação progressiva e recursos bundled. Use quando o usuário quer criar, escrever ou construir um novo skill.
---

# Writing Skills

## Processo

1. **Coletar requisitos** - pergunte ao usuário sobre:
   - Qual tarefa/dominio o skill cobre?
   - Quais casos de uso específicos ele deve lidar?
   - Precisa de scripts executáveis ou apenas instruções?
   - Algum material de referência para incluir?

2. **Rascunhar o skill** - crie:
   - SKILL.md com instruções concisas
   - Arquivos de referência adicionais se conteúdo exceder 500 linhas
   - Scripts utilitários se operações determinísticas forem necessárias

3. **Revisar com usuário** - apresente rascunho e pergunte:
   - Isto cobre seus casos de uso?
   - Algo faltando ou não claro?
   - Alguma seção deveria ser mais/menos detalhada?

## Estrutura de Skill

```
skill-name/
├── SKILL.md           # Instruções principais (obrigatório)
├── REFERENCE.md       # Docs detalhadas (se necessário)
├── EXAMPLES.md        # Exemplos de uso (se necessário)
└── scripts/           # Scripts utilitários (se necessário)
    └── helper.js
```

## Template SKILL.md

```md
---
name: skill-name
description: Breve descrição da capacidade. Use quando [triggers específicos].
---

# Skill Name

## Quick start

[Exemplo mínimo funcional]

## Workflows

[Processos passo-a-passo com checklists para tarefas complexas]

## Advanced features

[Link para arquivos separados: Veja [REFERENCE.md](REFERENCE.md)]
```

## Requisitos de Descrição

A descrição é **a única coisa seu agent vê** ao decidir qual skill carregar. É exibida no system prompt junto com todos os outros skills instalados. Seu agent lê estas descrições e escolhe o skill relevante baseado no request do usuário.

**Objetivo**: Dê ao seu agent informação suficiente para saber:

1. Qual capacidade este skill provê
2. Quando/por que trigger (palavras-chave específicas, contextos, tipos de arquivo)

**Formato**:

- Max 1024 chars
- Escreva em terceira pessoa
- Primeira frase: o que faz
- Segunda frase: "Use quando [triggers específicos]"

**Bom exemplo**:

```
Extrai texto e tabelas de arquivos PDF, preenche formulários, mescla documentos. Use quando trabalhando com arquivos PDF ou quando usuário menciona PDFs, formulários ou extração de documentos.
```

**Mau exemplo**:

```
Ajuda com documentos.
```

O mau exemplo não dá ao seu agent nenhuma forma de distinguir este skill de outros de documentos.

## Quando Adicionar Scripts

Adicione scripts utilitários quando:

- Operação é determinística (validação, formatação)
- Mesmo código seria gerado repetidamente
- Erros precisam de handling explícito

Scripts economizam tokens e melhoram confiabilidade vs código gerado.

## Quando Dividir Arquivos

Divida em arquivos separados quando:

- SKILL.md excede 100 linhas
- Conteúdo tem domínios distintos (financeiro vs schemas de vendas)
- Features avançadas são raramente necessárias

## Review Checklist

Após rascunhar, verifique:

- [ ] Description inclui triggers ("Use quando...")
- [ ] SKILL.md abaixo de 100 linhas
- [ ] Sem informação sensível ao tempo
- [ ] Terminologia consistente
- [ ] Exemplos concretos incluídos
- [ ] Referências um nível de profundidade
