# Fase 3 — Frontend

Stack React/Next.js para senior. Projetos incrementais num app de referência.

## Tópicos

| Tópico | Objetivo senior | Prática sugerida |
| --- | --- | --- |
| **TypeScript** | strict mode, utility types, generics, type guards | Migrar JS → TS em módulo |
| **React** | hooks, composition, perf (memo, useMemo), error boundaries | Feature com estado complexo |
| **Next.js** | App Router, RSC vs client, SSR/SSG, routing, middleware | App com auth + data fetching |
| **Tailwind / shadcn** | design system, a11y básica, theming | UI kit consistente |
| **TanStack Query** | cache, invalidation, optimistic updates, suspense | CRUD com server state |
| **Zustand** | client state mínimo vs server state | Store para UI global leve |
| **RHF + Zod** | forms complexos, validation schema | Form multi-step |
| **Vitest / RTL** | unit + component tests, user-centric queries | Cobertura de flows críticos |
| **Playwright** | e2e, fixtures, trace | Happy path + edge e2e |
| **Performance** | Core Web Vitals, bundle, lazy load, profiling | Lighthouse audit + fixes |
| **SEO** | metadata, OG, sitemap, structured data | Páginas públicas otimizadas |
| **React Native** | shared logic, navigation, platform diffs | Screen simples ou Expo spike |

## Projeto integrador sugerido

Dashboard SaaS: Next.js + shadcn + TanStack Query + auth + testes (Vitest + Playwright).

## Integração

- Spec de features → `tlc-spec-driven`
- Performance → Chrome DevTools / Lighthouse MCP se disponível

## Checkpoint

Explicar quando usar TanStack Query vs Zustand; trade-off RSC vs client component numa feature real.
