# ADR-003: Testing Seams

**Status:** Accepted  
**Date:** 2026-06-17

## Context

El portfolio comprende 16 proyectos con diferentes tipos de código: utilities puras, componentes de UI, API Routes de Next.js, y un paquete npm publicado. Se necesita una estrategia de testing consistente que aplique a todos los proyectos.

## Decision

Cuatro seams de testing, en orden de preferencia (usar la seam más alta posible):

### Seam 1: `lib/` utilities → Vitest unit tests
Funciones puras y lógica determinista. Para módulos que tocan proveedores externos (Claude, Cloudinary, Supabase), se separa la lógica pura de la llamada al proveedor — solo la capa pura tiene unit tests.

### Seam 2: Components → Storybook + axe-core + Testing Library
- Storybook documenta variantes visuales de cada componente.
- axe-core corre automáticamente contra cada story para detectar violaciones de accesibilidad.
- Testing Library se usa para componentes interactivos (filtros, dropdowns, modales, formularios, carrito) — afirmando sobre output visible, no estado interno.

### Seam 3: API Routes → integration tests contra route handlers reales
Los route handlers se testean con requests/responses realistas contra el código real. La lógica principal de la app no se mockea. Servicios externos que no son el sistema bajo test (Stripe, Anthropic, Resend, Supabase, Cloudinary) pueden controlarse con test mode, fixtures o mocks seguros.

**Precedente:** el proyecto le-point-du-fle estableció que mockear la capa de datos produce falsa confianza — tests pasan en local, fallan en producción.

### Seam 4: npm package → CI gate antes de publish
Pipeline bloqueante antes de cada `npm publish`: `typecheck → lint → build → Vitest → selected snapshots → Storybook build → axe-core`.

Los snapshots son señal de detección de cambios inesperados, no árbitro de calidad. Un snapshot fallido = revisar, no revertir automáticamente.

## Consequences

**Positivo:**
- Cada tipo de código tiene una seam natural y conocida desde el inicio del proyecto.
- Los tests de integración sobre route handlers reales eliminan la clase de bugs que los mocks ocultan.
- axe-core en Storybook convierte la accesibilidad en un artefacto continuo, no una auditoría eventual.

**Negativo:**
- Los integration tests de API Routes requieren configuración de entornos de test (Stripe test mode, Supabase test project, etc.).
- Storybook + axe-core añade setup inicial a cada proyecto de design system.
