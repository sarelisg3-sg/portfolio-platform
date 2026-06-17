# ADR-001: No Monorepo

**Status:** Accepted  
**Date:** 2026-06-17

## Context

El portfolio está compuesto por 16 proyectos independientes en 4 fases. Existe la opción de organizarlos en un monorepo (Turborepo, Nx) para compartir configuración, dependencias y tooling desde un solo lugar.

## Decision

Cada proyecto vive en su propio repositorio independiente bajo `sarelisg3-sg/`. No hay monorepo.

## Consequences

**Positivo:**
- Cada proyecto es un case study autónomo con su propia URL de deployment, README y historial de git limpio.
- El portfolio en GitHub muestra 16+ repos activos — más visible como evidencia de trabajo.
- Sin overhead de configuración de workspace de monorepo al iniciar cada proyecto.
- Cada repo puede tener sus propias decisiones de stack sin afectar a los demás.

**Negativo:**
- Duplicación de configuración base (tsconfig, eslint, tailwind) entre proyectos.
- Sin compartición de paquetes internos a través de workspace linking.

**Mitigación:** `portfolio-platform` centraliza las decisiones de stack en `AGENTS.md` como referencia autoritativa. Cada proyecto nuevo arranca desde esa referencia, no desde cero.
