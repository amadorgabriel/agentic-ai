# Fase 2 — Engenharia base

Disciplina de software e design de sistemas. Projetos sandbox recomendados.

## Tópicos

| Tópico | Objetivo senior | Prática sugerida |
| --- | --- | --- |
| **Clean Code** | naming, funções pequenas, SRP no método | Refactor de módulo legado |
| **SOLID** | 5 princípios com exemplos em TS/C# | Identificar violações em PR |
| **Patterns** | strategy, factory, observer, adapter — quando usar | Aplicar 2 patterns em projeto pequeno |
| **Clean Architecture** | camadas, dependência inward, ports/adapters | Esboçar boundaries de um serviço |
| **DDD** | bounded context, aggregates, ubiquitous language | skill pessoal `domain-modeling` + CONTEXT.md |
| **Arquitetura** | monolith modular, microservices trade-offs, event-driven intro | ADR comparando opções |
| **System Design** | scaling, CAP, load balancer, cache, DB choice | 3 cenários: URL shortener, feed, checkout |
| **Testes** | pirâmide, unit/integration/e2e, test doubles | Cobrir módulo com testes meaningful |
| **TDD** | red-green-refactor, quando vale a pena | TDD em módulo greenfield pequeno |

## Postergado

**CQRS** → [DEFERRED.md](../DEFERRED.md) — retomar após DDD sólido

## Integração

- DDD → `domain-modeling` skill
- System Design → oferecer `grilling` antes de `solid`
- Projetos grandes → `tlc-spec-driven`

## Checkpoint

Desenhar sistema de pedidos (monolith vs services) com cache, fila e DB — 30 min whiteboard.
