# Portfolio Platform

Hub central de documentación, decisiones de arquitectura, PRD y roadmap del portfolio profesional de Sareli García — UI/UX · Frontend · AI Engineer.

Este repositorio no contiene código de producción. Es la fuente de verdad para la estrategia, las decisiones técnicas y el estado de los 16 proyectos del portfolio.

---

## Proyectos

| # | Proyecto | Fase | Repo | Estado |
|---|----------|------|------|--------|
| 1 | Design System Personal | 1 | — | Por empezar |
| 2 | Portfolio V1 | 1 | — | Por empezar |
| 3 | Landing con Animaciones | 1 | — | Por empezar |
| 4 | Rediseño de App Existente | 1 | — | Por empezar |
| 5 | Dashboard de Analytics | 2 | — | Por empezar |
| 6 | E-commerce UI | 2 | — | Por empezar |
| 7 | App Colaborativa en Tiempo Real | 2 | — | Por empezar |
| 8 | Component Library Pública (npm) | 2 | — | Por empezar |
| 9 | Chat UI con Streaming | 3 | — | Por empezar |
| 10 | AI Design Token Generator | 3 | — | Por empezar |
| 11 | UX Reviewer con AI | 3 | — | Por empezar |
| 12 | AI Copy Generator para UI | 3 | — | Por empezar |
| 13 | Portfolio V2 con AI | 4 | — | Por empezar |
| 14 | Design Critique Tool (SaaS) | 4 | — | Por empezar |
| 15 | UI Generator desde Prompts | 4 | — | Por empezar |
| 16 | AI Design System Docs | 4 | — | Por empezar |

---

## Documentación

- [PRD: Portfolio Platform](docs/prd/PRD-001-portfolio-platform.md)
- [Roadmap de Proyectos](docs/roadmap/roadmap-proyectos.md)
- [Stack Reference (AGENTS.md)](AGENTS.md)
- [ADR-001: No Monorepo](docs/adr/ADR-001-no-monorepo.md)
- [ADR-002: GitHub-first Deploy](docs/adr/ADR-002-github-first-deploy.md)
- [ADR-003: Testing Seams](docs/adr/ADR-003-testing-seams.md)

---

## Cómo se relaciona con los repositorios de proyectos

Cada proyecto del portfolio vive en su propio repositorio independiente bajo `sarelisg3-sg/`. Cada repo de proyecto:

- Tiene su propio README, issues, CI y deployment en Vercel
- Linkea al issue de kickoff en este repositorio
- Sigue el stack y convenciones definidos en [AGENTS.md](AGENTS.md)

El flujo estándar de desarrollo es:

```
git push origin main
       ↓
GitHub Actions CI (typecheck → lint → test)
       ↓ (si CI pasa)
Vercel GitHub App
       ↓
Deploy automático a producción
```

---

## Proyectos existentes

| Proyecto | Repo | Notas |
|----------|------|-------|
| le-point-du-fle-next | sarelisg3-sg/le-point-du-fle | Conversión HTML → Next.js desplegada. Pendiente migrar a GitHub-first deploy. |
| todo-app | — (local) | App mínima de referencia. No es un case study prioritario. |
