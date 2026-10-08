# Fase 6 — IA Aplicada

IA no ciclo de desenvolvimento e em produto. Alinhado ao ecossistema deste repositório (`agentic-ai`).

## Tópicos

| Tópico | Objetivo senior | Prática sugerida |
| --- | --- | --- |
| **Cursor / Copilot** | prompts eficazes, rules, skills, review assistido | Workflow diário documentado |
| **SDD** | Spec-Driven Development | skill pessoal `tlc-spec-driven` em feature real |
| **LLM fundamentals** | tokens, context window, temperature, model selection | Comparar 2 modelos numa tarefa |
| **Semantic Kernel** | plugins, planners, .NET integration | Orquestrador simples em C# |
| **RAG / pgvector** | chunking, embeddings, retrieval, grounding | Q&A sobre docs internos |
| **MCP** | tools, resources, auth | Consumir ou expor MCP server |
| **Agents** | tool calling, multi-step, guardrails | Agent com 2–3 tools |
| **Evals** | golden sets, regression, quality metrics | Eval suite para prompt/agent |
| **Langfuse** | tracing, cost, prompt versioning | Instrumentar pipeline RAG |
| **Ollama** | local models, privacy, dev offline | Rodar modelo local para dev |
| **LGPD** | dados pessoais, consent, retention, DPIA básico | Checklist em feature com PII |

## Projeto integrador sugerido

Assistente interno: RAG (pgvector) + agent MCP + evals + Langfuse + deploy .NET.

## Integração

- Esta fase reforça o próprio repo `agentic-ai` (skills, agents)
- SDD → skill nativa do repo

## Checkpoint

Desenhar pipeline RAG com failure modes; quando usar agent vs chain; implicações LGPD para logs de chat.
