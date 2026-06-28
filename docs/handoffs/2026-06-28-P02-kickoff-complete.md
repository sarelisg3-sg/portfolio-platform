# Handoff — P02 Portfolio V1 · Kickoff Complete

**Fecha:** 2026-06-28  
**Sesión:** P02 — Construcción y QA de portfolio-v1  
**Estado:** Kickoff completo · CI verde · GitHub ↔ Vercel activo · Listo para contenido

---

## Contexto

Este handoff cierra la fase de kickoff de P02 Portfolio V1. El portfolio está en producción, trilingüe (ES/EN/FR), con CI pasando y auto-deploy desde GitHub configurado. La sesión anterior (2026-06-27-P02-kickoff.md) cubre la propuesta de scope y schema MDX. Esta sesión cubre la implementación completa y el QA.

---

## Artefactos clave

| Artefacto | URL / Ruta |
|---|---|
| Repo GitHub | https://github.com/sarelisg3-sg/portfolio-v1 |
| Deploy producción | https://portfolio-v1-zeta-liart.vercel.app |
| Issue #3 (kickoff) | https://github.com/sarelisg3-sg/portfolio-platform/issues/3 |
| projects.json | `portfolio-platform/projects.json` — portfolio-v1 en `in-progress` |
| Handoff anterior | `docs/handoffs/2026-06-27-P02-kickoff.md` |

---

## Stack final

| Tecnología | Versión / Detalle |
|---|---|
| Next.js | 16.2.9 — App Router, `proxy.ts` (no middleware.ts) |
| next-intl | 4.x — `defineRouting`, `getRequestConfig`, `createMiddleware` |
| Tailwind CSS | v4 — CSS custom properties (`var(--accent)`, etc.) |
| TypeScript | strict, sin `any` |
| MDX | `next-mdx-remote/rsc` + `gray-matter` |
| Resend | Preparado, no-blocking si falta `RESEND_API_KEY` |
| Node.js (CI) | 24 (alineado con entorno local — ver decisión abajo) |

**Convención importante:** Next.js 16 renombró `middleware.ts` → `proxy.ts`. No revertir.

---

## Estructura de archivos clave

```
portfolio-v1/
├── proxy.ts                          # Middleware i18n (Next.js 16)
├── next.config.ts                    # withNextIntl plugin
├── lib/i18n/routing.ts               # locales: ["es", "en", "fr"], defaultLocale: "es"
├── lib/i18n/request.ts               # getRequestConfig → messages/[locale].json
├── lib/mdx.ts                        # getProject(), getAllProjects(), getFeaturedProjects()
├── types/project.ts                  # ProjectFrontmatter, ProjectType, ProjectStatus
├── messages/
│   ├── es.json                       # Completo, sin TODOs
│   ├── en.json                       # Completo, sin TODOs
│   └── fr.json                       # Completo, sin TODOs
├── content/projects/
│   ├── le-point-du-fle/{es,en,fr}.mdx
│   └── artium-online/{es,en,fr}.mdx
├── public/projects/
│   ├── le-point-du-fle/cover.png     # ⚠️ FALTA — ver pendientes
│   └── artium-online/cover.png       # ⚠️ FALTA — ver pendientes
├── app/
│   ├── layout.tsx                    # Root mínimo (sin html tag)
│   └── [locale]/
│       ├── layout.tsx                # NextIntlClientProvider + Inter + Navbar + Footer
│       ├── page.tsx                  # Hero + proyectos destacados + About
│       ├── contact/page.tsx
│       └── projects/[slug]/page.tsx
├── components/
│   ├── layout/{Navbar,Footer}.tsx
│   ├── projects/ProjectCard.tsx
│   └── contact/ContactForm.tsx
├── app/api/contact/route.ts          # Resend POST, 503 sin API key
└── .github/workflows/ci.yml         # Node 24 — typecheck · lint · build
```

---

## i18n — Rutas verificadas en producción

| Ruta | Status | Título `<title>` |
|---|---|---|
| `/es` | ✅ 200 | Sareli Santiago García — Diseñadora UI/UX & AI Engineer |
| `/en` | ✅ 200 | Sareli Santiago García — UI/UX Designer & AI Engineer |
| `/fr` | ✅ 200 | Sareli Santiago García — Designer UI/UX & ingénieure IA |
| `/es/projects/le-point-du-fle` | ✅ 200 | Rediseño de Le Point du FLE — Sareli Santiago García |
| `/es/projects/artium-online` | ✅ 200 | Artium Online — Sareli Santiago García |
| `/es/contact` | ✅ 200 | Contacto — Sareli Santiago García |
| `/en/contact` | ✅ 200 | Contact — Sareli Santiago García |
| `/fr/contact` | ✅ 200 | Contact — Sareli Santiago García |

hreflang `es/en/fr/x-default` presentes en todas las rutas. Locale switcher preserva ruta actual.

---

## Proyectos MDX — Schema

```typescript
interface ProjectFrontmatter {
  slug: string;
  locale: "es" | "en" | "fr";
  title: string;
  tagline: string;
  date?: string;           // opcional — Artium Online no tiene fecha
  status: "done" | "in-progress" | "concept";
  type: "redesign" | "frontend" | "ux-case-study" | "external" | "design-system";
  tags: string[];
  featured: boolean;
  liveUrl?: string;
  repoUrl?: string;
  legacyRepoUrl?: string;
  externalUrl?: string;
  coverImage?: string;
  coverAlt?: string;
  description: string;
}
```

---

## Case studies iniciales

### Le Point du FLE (`content/projects/le-point-du-fle/`)
- **Type:** `redesign` · **Status:** `in-progress`
- **Date:** `2026-06`
- **Links:** liveUrl + legacyRepoUrl (GitHub versión HTML original)
- **MDX:** Case study completo en ES (El problema → El enfoque → Stack → Estado actual). EN y FR disponibles.
- **Cover:** ⚠️ Falta screenshot

### Artium Online (`content/projects/artium-online/`)
- **Type:** `external` · **Status:** `done`
- **Sin campo `date`** (omitido intencionalmente — no inventar fecha)
- **Links:** solo externalUrl → `https://www.artiumonline.com/`
- **MDX:** Contenido provisional mínimo (2 secciones). Expandir con datos reales cuando estén disponibles.
- **Cover:** ⚠️ Falta screenshot

---

## CI — Estado

**Verde.** Último run exitoso: `28310420832`

```yaml
# .github/workflows/ci.yml
node-version: 24   # ← Node 24, no 22 (ver decisión)
steps: npm ci → tsc --noEmit → npm run lint → npm run build
```

---

## GitHub ↔ Vercel — Integración

**Activa y verificada.**

- Repo conectado: `sarelisg3-sg/portfolio-v1` → proyecto `portfolio-v1` en Vercel
- Primer auto-deploy confirmado: commit `834d7b7` → deploy `dpl_97xbFb9YKRKiS53nSCa65nMk7ZqF` → READY
- Flujo: `git push origin main` → GitHub Actions (CI) → Vercel auto-deploy

**Nota:** GitHub App de Vercel está en modo `Only select repositories`. Al conectar repos futuros, hay que añadirlos manualmente en `github.com/settings/installations` → Vercel → Configure.

---

## Decisiones tomadas

| Decisión | Razón |
|---|---|
| `proxy.ts` en lugar de `middleware.ts` | Next.js 16 depreca la convención `middleware` — advertencia en build |
| CI en Node 24 (no 22) | Node 22 (npm 10) resolvía `@swc/helpers@0.5.23` pero el lock file generado localmente con npm 11 (Node 24) tenía `0.5.15` — divergencia causaba `npm ci` failure |
| Artium Online sin campo `date` | Campo `date?` es opcional en el schema — no inventar fechas |
| Resend no-blocking | Si `RESEND_API_KEY` no está seteada, API devuelve 503 sin romper el deploy |
| `contact_title` / `projects_title` solo nombre corto en messages | El layout aplica template `%s — Sareli Santiago García` — incluir el sufijo en el valor causaba título duplicado |
| `.vercel/project.json` commiteado | Regla en AGENTS.md del proyecto |
| next-intl 4.x (no i18n manual) | Decisión de scope aprobada por usuaria en sesión anterior |

---

## Pendientes — Próxima sesión

### Bloqueantes para mostrar a reclutadores

1. **Cover images** — Tomar screenshots de:
   - `https://www.artiumonline.com/` → `public/projects/artium-online/cover.png`
   - `https://le-point-du-fle-next-jkjxovbju-sare1.vercel.app` → `public/projects/le-point-du-fle/cover.png`
   - Resolución recomendada: 1280×720 PNG
   - Después de añadir: `git push origin main` → auto-deploy activo

2. **Configurar dominio custom** en Vercel dashboard (cuando esté disponible `sareli.dev` u otro)

### No bloqueantes

3. **Resend API key** — Añadir `RESEND_API_KEY` en Vercel dashboard → Settings → Environment Variables cuando esté lista
4. **Expandir case study Artium Online** — El cuerpo MDX tiene solo 2 párrafos provisionales. Completar con detalle real del proyecto cuando esté disponible
5. **Conectar le-point-du-fle-next a GitHub** — El repo de ese proyecto está local sin remote conectado
6. **Git identity** — Configurar `git config --global user.name` y `user.email` para evitar la advertencia en cada commit

---

## Variables de entorno

```bash
# .env.local.example (ya existe en repo)
RESEND_API_KEY=     # Formulario de contacto — sin esto devuelve 503
ANTHROPIC_API_KEY=  # Reservado para fases futuras
```

---

## Comandos útiles

```bash
# Desarrollo local
cd "/Users/sarelisantiagogarcia/vercel test/portfolio-v1"
npm run dev

# Deploy manual (si se necesitara)
npx vercel deploy --prod

# CI local
npx tsc --noEmit && npm run lint && npm run build
```

---

## Suggested skills

Para la próxima sesión:

- `/handoff` — Al cerrar la sesión de covers
- `/qa` — Para verificar que las covers se muestran correctamente en todas las rutas y locales
- `/to-issues` — Si se quiere convertir los pendientes en issues de GitHub
