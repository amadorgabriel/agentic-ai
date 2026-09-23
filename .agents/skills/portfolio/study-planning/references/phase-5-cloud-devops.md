# Fase 5 — Cloud & DevOps

Deploy, observabilidade e pipeline. Foco AWS + containers (K8s postergado).

## Tópicos

| Tópico | Objetivo senior | Prática sugerida |
| --- | --- | --- |
| **AWS** | EC2/ECS or Lambda, RDS, S3, IAM, VPC básico | Deploy app Fase 3/4 em AWS |
| **Docker** | Dockerfile multi-stage, compose, images slim | Containerizar API + frontend |
| **GitHub Actions** | CI/CD, matrix, secrets, deploy gate | Pipeline test → build → deploy |
| **Sentry** | error tracking, releases, breadcrumbs | Integrar frontend + backend |
| **OpenTelemetry** | traces, metrics, logs correlation | Trace request end-to-end |

## Postergados

- **Kubernetes** → [DEFERRED.md](../DEFERRED.md)
- **Terraform** → [DEFERRED.md](../DEFERRED.md)

## Projeto integrador sugerido

Mesmo app das Fases 3–4: Docker Compose local → GitHub Actions → AWS (ECS ou App Runner) + Sentry + OTel.

## Integração

- Cloudflare Workers skills disponíveis no ambiente — comparar quando serverless edge faz sentido vs AWS default do roadmap

## Checkpoint

Explicar IAM least privilege para deploy CI; diferença logs vs metrics vs traces com exemplo.
