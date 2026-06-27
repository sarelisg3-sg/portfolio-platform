# Handoff — 2026-06-27

## Contexto

Working directory: `/Users/sarelisantiagogarcia/vercel test`  
Sesión anterior (2026-06-24): creó `portfolio-platform`, publicó 17 issues de kickoff, tomó decisiones de arquitectura.  
Esta sesión (2026-06-27): arrancó y completó los **4 primeros commits de P01 (Design System Personal)**, conectó Vercel y publicó Storybook.

---

## Estado actual

### Repo P01
**`sarelisg3-sg/design-system`** — público, rama `main`  
https://github.com/sarelisg3-sg/design-system

### Storybook público
**https://design-system-sare1.vercel.app**  
Estado: `READY` · Auto-deploy desde `main` activo.

### Hub central
**`sarelisg3-sg/portfolio-platform`** — sin cambios en esta sesión  
https://github.com/sarelisg3-sg/portfolio-platform  
`projects.json` todavía tiene `design-system` en status `"not-started"` — pendiente de actualizar.

---

## Commits realizados esta sesión

| Hash | Mensaje | Propósito |
|------|---------|-----------|
| `ab1a303` | `feat: init Next.js 16 + Tailwind v4 + shadcn/ui + CI` | Scaffold base con create-next-app, shadcn init, GitHub Actions CI (typecheck → lint → build), AGENTS.md y README |
| `1d7ba00` | `feat(tokens): define design foundations en globals.css` | Tokens de diseño como CSS custom properties `--ds-*` en `app/globals.css`: brand (11 pasos), neutral (11 pasos), semantic state (success/warning/error/info), tipografía (Major Third ×1.250), radios, sombras |
| `544112f` | `feat(storybook): Storybook 10 + Button, Input, Badge` | Storybook 10 (nextjs-vite), 3 componentes con stories, addon-a11y en modo error, addon-vitest + Playwright |
| `db80652` | `chore(vercel): add vercel.json con build config explícita` | Resolvió el fallo de Vercel por espacio accidental en el dashboard |

---

## Stack del proyecto

| Herramienta | Versión | Rol |
|---|---|---|
| Next.js | 16.2.9 | Entorno de desarrollo (no se despliega) |
| React | 19.2.4 | Framework |
| TypeScript | ^5 | Tipado |
| Tailwind CSS | ^4 | CSS-first, sin `tailwind.config.ts` |
| shadcn/ui | 4.11.0 | Infraestructura (CVA, clsx, tailwind-merge) |
| Storybook | 10.4.6 | Entregable público |
| Vitest + Playwright | ^4.1.9 | Test runner de stories (browser) |

---

## Estructura local

```
/Users/sarelisantiagogarcia/vercel test/design-system/
├── app/
│   ├── globals.css         ← fuente de verdad de tokens (--ds-*)
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── Button/
│   │   ├── Button.tsx      ← 5 variantes × 3 tamaños, usa tokens
│   │   └── Button.stories.tsx
│   ├── Input/
│   │   ├── Input.tsx       ← label, error state, disabled, aria-*
│   │   └── Input.stories.tsx
│   └── Badge/
│       ├── Badge.tsx       ← 5 variantes, usa tokens muted
│       └── Badge.stories.tsx
├── components/ui/
│   └── button.tsx          ← generado por shadcn (no tocar)
├── lib/
│   └── utils.ts            ← cn() helper
├── .storybook/
│   ├── main.ts             ← framework: nextjs-vite, stories: components/**
│   └── preview.tsx         ← importa globals.css, a11y: error
├── .github/workflows/
│   └── ci.yml              ← typecheck → lint → build
├── vercel.json             ← buildCommand + outputDirectory explícitos
├── vitest.config.ts        ← Storybook + Playwright browser tests
├── AGENTS.md               ← stack reference del proyecto
└── README.md
```

---

## Configuración de Storybook

- **Framework**: `@storybook/nextjs-vite` (Vite, no webpack)
- **Addons**: `addon-a11y` · `addon-vitest` · `addon-docs` · `addon-mcp` · `@chromatic-com/storybook`
- **Stories path**: `components/**/*.stories.@(js|jsx|mjs|ts|tsx)`
- **a11y mode**: `"error"` — CI falla en violaciones de accesibilidad
- **globals.css**: importado en `preview.tsx` → tokens `--ds-*` disponibles en todas las stories
- **Import**: `from "@storybook/nextjs-vite"` (NO `@storybook/react` — rompe el ESLint plugin)

---

## Configuración de Vercel

- **Proyecto**: `design-system` en team `sare` (Hobby)
- **Project ID**: `prj_9qlK1JD0qpmYwNZgzb60MwjNdTej`
- **Build command**: `npm run build-storybook` (definido en `vercel.json`)
- **Output directory**: `storybook-static` (definido en `vercel.json`)
- **Framework preset**: Other
- **Deploy trigger**: push a `main` (GitHub integration activa)
- **Dominios**:
  - `design-system-sare1.vercel.app` (producción)
  - `design-system-git-main-sare1.vercel.app` (alias de rama)

---

## Estado del CI

Todos los runs en **success**. Los 4 commits pasaron CI en GitHub Actions.

| Commit | Run ID | Estado | Duración |
|---|---|---|---|
| `db80652` | — | success | ~40s |
| `544112f` | 28275993501 | success | 41s |
| `1d7ba00` | 28274285901 | success | 40s |
| `ab1a303` | 28140764588 | success | 43s |

---

## Tokens definidos (`app/globals.css`)

- **`--ds-brand-{50..950}`** — escala violeta 11 pasos (oklch, hue 293 — placeholder, reemplazable)
- **`--ds-neutral-{50..950}`** — escala gris 11 pasos
- **`--ds-success/warning/error/info`** — colores de estado semántico
- **`--ds-success/warning/error/info-muted`** — versiones suaves para Badge
- **`--ds-text-{2xs..3xl}`** — escala de tipografía Major Third ×1.250
- **`--ds-weight-{regular/medium/semibold/bold}`** — pesos
- **`--ds-leading-{none..loose}`** — line heights
- **`--ds-tracking-{tighter..widest}`** — letter spacing
- **`--ds-radius-{none..full}`** — border radii
- **`--ds-shadow-{xs..2xl,inner}`** — sombras

Brand + state colors mapeados en `@theme inline` → generan utilidades Tailwind (`bg-brand-500`, `text-error`, etc.)

**`lib/tokens.ts` NO existe** — aplazado a P08 o cuando haya necesidad real desde TypeScript.

---

## Problemas encontrados y resueltos

### 1. ESLint error en stories (commit 3)
**Error**: `storybook/no-renderer-packages` — las stories importaban `from "@storybook/react"`.  
**Fix**: cambiar a `from "@storybook/nextjs-vite"` en los 3 archivos `.stories.tsx`.

### 2. Primer deploy de Vercel falló
**Error**: `No Output Directory named " storybook-static" found` (espacio accidental en el campo del dashboard).  
**Fix**: crear `vercel.json` con `buildCommand` y `outputDirectory` explícitos en el repo. Evita depender del dashboard.

---

## Decisiones arquitectónicas importantes

Todas las decisiones del PRD y ADRs siguen vigentes (ver `portfolio-platform`). Decisiones tomadas en **esta sesión**:

1. **`lib/tokens.ts` aplazado** — `globals.css` es única fuente de verdad hasta P08. No crear el mirror TypeScript sin necesidad real demostrada.
2. **`vercel.json` en el repo** — build config explícita en el código, no en el dashboard.
3. **Tokens con prefijo `--ds-*`** — evita colisiones con variables de shadcn (`--primary`, etc.)
4. **Tokens muted como parte del sistema** — `--ds-success-muted` etc. son tokens de primera clase necesarios para Badge, no workarounds.

---

## Qué quedó pendiente

### Checklist del issue #2 (P01 kickoff)
- [x] Repo creado en GitHub (`sarelisg3-sg/design-system`)
- [x] CI configurado (typecheck → lint → build)
- [x] Vercel conectado vía GitHub integration
- [x] README con descripción y link al issue
- [x] Primer deploy de Storybook en producción
- [ ] Componentes MVP restantes: **Textarea, Card, Avatar, Modal, Typography** (faltan 5 de 8)
- [ ] Case study documentado en MDX
- [ ] Link agregado al portfolio principal (cuando exista P02)
- [ ] `projects.json` actualizado en `portfolio-platform`

### Estado del design system
- **Implementados**: Button, Input, Badge
- **Pendientes**: Textarea, Card, Avatar, Modal, Typography

---

## Próximo paso recomendado

Continuar con los 5 componentes MVP restantes **de a uno o dos por commit**, siguiendo el mismo patrón:

1. Crear `components/<Name>/<Name>.tsx`
2. Crear `components/<Name>/<Name>.stories.tsx`
3. Verificar: typecheck + lint + build + build-storybook
4. Commit y push

Orden sugerido (de menor a mayor complejidad):
1. **Textarea** — similar a Input, simple
2. **Card** — contenedor layout, sin lógica
3. **Avatar** — imagen + fallback
4. **Typography** — sistema de texto documentado
5. **Modal** — más complejo, requiere `"use client"` y gestión de focus trap

---

## Prompt para continuar

```
Vamos a continuar con P01: Design System Personal.

Repo local: /Users/sarelisantiagogarcia/vercel test/design-system
Repo GitHub: https://github.com/sarelisg3-sg/design-system
Storybook en producción: https://design-system-sare1.vercel.app

Estado actual:
- 4 commits hechos, todos en CI success
- Storybook desplegado y funcionando
- Componentes implementados: Button, Input, Badge
- Tokens definidos en app/globals.css (prefijo --ds-*)
- lib/tokens.ts NO existe — aplazado hasta P08

Actúa como Senior Frontend Engineer + Design Systems Engineer.

El siguiente paso es implementar los 5 componentes MVP restantes:
Textarea, Card, Avatar, Typography, Modal

Antes de escribir código:
1. Lee AGENTS.md en el repo design-system
2. Lee app/globals.css para ver los tokens disponibles
3. Lee components/Button/Button.tsx como referencia de patrones

Reglas de scope:
- Un componente por commit (o dos si son muy simples y relacionados)
- Verificar typecheck + lint + build + build-storybook antes de cada commit
- No crear lib/tokens.ts
- No agregar dependencias nuevas sin justificación
- Modal va último por ser el más complejo

Empieza por Textarea.
```

---

## Suggested skills

| Skill | Cuándo usarlo |
|-------|---------------|
| `/verify` | Después de cada componente, para confirmar que Storybook en Vercel renderiza correctamente |
| `/code-review` | Antes de dar P01 por terminado, revisar consistencia entre los 5 componentes |
| `/run` | Para correr Storybook localmente y hacer QA visual antes del push |
| `/to-issues` | Si se quiere descomponer los 5 componentes restantes en issues dentro del repo `design-system` |
