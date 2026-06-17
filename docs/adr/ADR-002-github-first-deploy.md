# ADR-002: GitHub-first Deploy

**Status:** Accepted  
**Date:** 2026-06-17

## Context

Los proyectos existentes (todo-app, le-point-du-fle-next) se desplegaron directamente via `npx vercel deploy --yes` sin integración con GitHub. Esto funciona pero elimina los preview deployments, el CI previo al deploy, y la trazabilidad entre commits y deployments.

## Decision

Todos los proyectos nuevos usan el flujo GitHub-first:

1. `git push origin main` (o PR merge)
2. GitHub Actions CI corre: `typecheck → lint → test`
3. Si CI pasa, Vercel GitHub App despliega automáticamente
4. Cada PR genera un Preview Deployment con su propia URL

El comando `npx vercel deploy --yes` queda reservado solo para deploys de emergencia manuales.

## Consequences

**Positivo:**
- Cada deploy queda vinculado a un commit específico.
- Los PRs tienen preview deployments automáticos.
- El CI bloquea deploys de código roto antes de que lleguen a producción.
- La integración Vercel + GitHub muestra deployment status directamente en los PRs.

**Negativo:**
- Los proyectos existentes (`le-point-du-fle-next`) necesitan migración: conectar el repo a Vercel via GitHub integration y agregar el workflow de CI.

**Para proyectos existentes:** migrar cuando haya un cambio significativo que amerite el setup. No bloquear desarrollo nuevo por la migración.
