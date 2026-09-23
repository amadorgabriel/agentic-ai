# Fase 4 — Backend .NET

API production-grade com ASP.NET Core e ecossistema.

## Tópicos

| Tópico | Objetivo senior | Prática sugerida |
| --- | --- | --- |
| **ASP.NET Core** | minimal APIs vs controllers, DI, middleware, config | API REST versionada |
| **PostgreSQL / EF Core** | migrations, relationships, performance, raw SQL quando necessário | Modelagem + queries N+1 fix |
| **Redis** | cache, session, rate limit, pub/sub básico | Cache de leitura quente |
| **Hangfire** | background jobs, retries, dashboard | Job recorrente + fila |
| **RabbitMQ** | exchanges, queues, dead letter, idempotência | Producer/consumer async |
| **SignalR** | hubs, groups, scale-out awareness | Notificações real-time |
| **Auth JWT / OAuth** | tokens, refresh, OIDC flow, policies | Auth completo com roles |
| **OWASP** | Top 10, input validation, SQLi, XSS, CSRF | Threat model + mitigações |

## Projeto integrador sugerido

API e-commerce/order: EF Core + Redis + Hangfire + RabbitMQ + JWT + SignalR para status.

## Integração

- DDD/Clean Arch (Fase 2) aplicados na solution structure
- OWASP → revisar com mindset de `code-review`

## Checkpoint

Desenhar fluxo auth (access + refresh); explicar quando Redis vs DB; idempotência em consumer RabbitMQ.
