---
name: design-an-interface
description: Gera designs de interface radicalmente diferentes para um módulo usando sub-agentes paralelos. Use quando o usuário quer projetar uma API, explorar opções de interface, comparar formatos de módulo, ou menciona "design it twice".
---

# Design an Interface

Baseado em "Design It Twice" do livro "A Philosophy of Software Design": sua primeira ideia provavelmente não é a melhor. Gere designs radicalmente diferentes e compare.

## Workflow

### 1. Gather Requirements

Antes de projetar, entenda:

- [ ] Qual problema este módulo resolve?
- [ ] Quem são os callers? (outros módulos, usuários externos, testes)
- [ ] Quais são as operações principais?
- [ ] Alguma restrição? (performance, compatibilidade, padrões existentes)
- [ ] O que deve ser escondido internamente vs exposto?

**IMPORTANTE - Quando não houver imagem na descrição da tarefa:**
Se a task do ClickUp não incluir uma imagem de referência da interface desejada:

1. **Analise o codebase frontend existente** - Explore a estrutura atual do projeto:
   - Veja módulos similares já implementados
   - Identifique padrões de componentes usados
   - Entenda a arquitetura de hooks (controllers, mutations, options)
   - Verifique como forms são estruturados (fieldsets, schemas)
   - Analise tipos TypeScript e organização

2. **Crie a interface baseada no código existente** - Use os padrões encontrados:
   - Siga a mesma estrutura de diretórios
   - Reutilize convenções de nomenclatura
   - Mantenha consistência com hooks controllers/mutations
   - Use componentes reutilizáveis existentes

3. **Pergunte ao usuário** - Após analisar:
   > "Não encontrei imagem de referência na task. Analisei o módulo [X] como referência de padrão. Posso criar a interface seguindo este modelo?"

Pergunte: "O que este módulo precisa fazer? Quem vai usar?"

### 2. Generate Designs (Sub-Agentes Paralelos)

Spawn 3+ sub-agentes simultaneamente usando Task tool. Cada um deve produzir uma abordagem **radicalmente diferente**.

```
Prompt template para cada sub-agent:

Design uma interface para: [descrição do módulo]

Requisitos: [requisitos coletados]

Constraints para este design: [assign uma constraint diferente para cada agent]
- Agent 1: "Minimize a contagem de métodos - mire 1-3 métodos max"
- Agent 2: "Maximize flexibilidade - suporte muitos casos de uso"
- Agent 3: "Otimize para o caso mais comum"
- Agent 4: "Tome inspiração de [paradigma/biblioteca específica]"

Output format:
1. Assinatura da interface (types/métodos)
2. Exemplo de uso (como o caller usa)
3. O que este design esconde internamente
4. Trade-offs desta abordagem
```

### 3. Apresentar Designs

Mostre cada design com:

1. **Assinatura da interface** - types, métodos, params
2. **Exemplos de uso** - como os callers realmente usam na prática
3. **O que esconde** - complexidade mantida interna

Apresente designs sequencialmente para o usuário absorver cada abordagem antes da comparação.

### 4. Comparar Designs

Depois de mostrar todos, compare por:

- **Simplicidade de interface**: menos métodos, params mais simples
- **Generalista vs especializado**: flexibilidade vs foco
- **Eficiência de implementação**: o formato permite internais eficientes?
- **Profundidade**: interface pequena escondendo complexidade significativa (bom) vs interface grande com implementação fina (ruim)
- **Facilidade de uso correto** vs **facilidade de uso errado**

Discuta trade-offs em prosa, não tabelas. Destaque onde os designs mais divergem.

### 5. Sintetizar

Frequentemente o melhor design combina insights de múltiplas opções. Pergunte:

- "Qual design melhor se encaixa no seu caso de uso principal?"
- "Algum elemento de outros designs vale incorporar?"

## Critérios de Avaliação

De "A Philosophy of Software Design":

**Simplicidade de interface**: Menos métodos, params simples = mais fácil de aprender e usar corretamente.

**Generalista**: Pode lidar com casos futuros sem mudanças. Mas cuidado com super-generalização.

**Eficiência de implementação**: O formato da interface permite implementação eficiente? Ou força internais estranhas?

**Profundidade**: Interface pequena escondendo complexidade significativa = módulo profundo (bom). Interface grande com implementação fina = módulo raso (evitar).

## Anti-Patterns

- Não deixe sub-agentes produzirem designs similares - enforce diferença radical
- Não pule a comparação - o valor está no contraste
- Não implemente - isto é puramente sobre formato da interface
- Não avalie baseado em esforço de implementação