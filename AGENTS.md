<!-- BEGIN:nextjs-agent-rules -->
# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.
<!-- END:nextjs-agent-rules -->

---

# Stack del Proyecto — Portfolio de Diseñadora + AI Engineer

Este proyecto es un portfolio profesional con AI integrada. Está diseñado para escalar desde un sitio estático hasta una plataforma con funcionalidades AI nativas. Todo corre en Vercel capa gratuita (Hobby).

---

## Framework & Routing

**Next.js 16+ (App Router)**
- Usar exclusivamente el App Router (`app/`). No usar `pages/`.
- Rutas dinámicas para proyectos: `app/projects/[slug]/page.tsx`
- Server Components por defecto; marcar `"use client"` solo cuando se necesite estado o eventos del browser.
- API Routes en `app/api/` para endpoints de AI y formularios.

---

## Estilos & UI

**Tailwind CSS v4**
- Configuración en `tailwind.config.ts`. Variables de tokens en `app/globals.css`.
- Clases utilitarias directamente en JSX, sin CSS modules salvo excepciones justificadas.

**shadcn/ui**
- Componentes base en `components/ui/`. No modificar los archivos generados por shadcn directamente; extenderlos en `components/`.
- Instalar nuevos componentes con `npx shadcn@latest add <componente>`.

**Framer Motion**
- Animaciones de entrada, transiciones de página y micro-interactions.
- Usar `<AnimatePresence>` para elementos que aparecen/desaparecen.
- Mantener `variants` en archivos separados en `lib/animations.ts` para reutilización.

**GSAP**
- Reservado para animaciones de scroll complejas y efectos de timeline.
- Usar `useGSAP()` del paquete `@gsap/react` para limpieza automática.
- No mezclar GSAP y Framer Motion sobre el mismo elemento.

---

## Contenido

**MDX**
- Los case studies de proyectos viven en `content/projects/*.mdx`.
- Los metadatos (título, fecha, tags, imagen cover) van en el frontmatter YAML.
- Procesado con `next-mdx-remote` o `@next/mdx`. Leer la configuración actual antes de agregar plugins de remark/rehype.
- Componentes custom disponibles en MDX están registrados en `lib/mdx-components.tsx`.

**Estructura de un case study:**
```
---
title: "Nombre del Proyecto"
date: "2025-01"
tags: ["branding", "ux", "web"]
cover: "/projects/nombre/cover.jpg"
summary: "Una línea que describe el proyecto."
---

Contenido en markdown con componentes custom embebidos.
```

---

## Media & Assets

**next/image**
- Usar siempre `<Image>` de `next/image` para imágenes del proyecto. Nunca `<img>` plano.
- Imágenes estáticas en `public/projects/<slug>/`.

**Cloudinary** (para imágenes de alta resolución)
- Las imágenes pesadas (galerías, mockups) se alojan en Cloudinary y se sirven con transformaciones on-the-fly.
- Helper en `lib/cloudinary.ts` para construir URLs con parámetros de transformación.
- Variables de entorno requeridas: `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`.

---

## Base de Datos & Backend

**Supabase**
- Usado para funcionalidades colaborativas y almacenamiento de datos de usuario.
- Cliente en `lib/supabase.ts` (server) y `lib/supabase-browser.ts` (client).
- Real-time con `supabase.channel()` para presencia y sincronización.
- Variables requeridas: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`.

---

## Capa AI

**Anthropic SDK / Claude**
- Modelo principal: `claude-haiku-4-5-20251001` para respuestas rápidas, `claude-sonnet-4-6` para análisis complejos.
- Streaming con Vercel AI SDK (`ai` package): usar `streamText()` de `@ai-sdk/anthropic`.
- Las llamadas a la API de Claude van SIEMPRE desde Server Components o API Routes, nunca exponer la API key al cliente.
- Variable requerida: `ANTHROPIC_API_KEY`.

**Vercel AI SDK**
- `useChat()` para interfaces de chat con streaming.
- `useCompletion()` para generaciones one-shot (copy, feedback de diseño).
- Handlers en `app/api/chat/route.ts` y `app/api/completion/route.ts`.

**RAG (Retrieval-Augmented Generation)**
- Embeddings generados con `text-embedding-3-small` de OpenAI o el modelo de embeddings de Cohere.
- Vectores almacenados en Supabase con la extensión `pgvector`.
- Pipeline: `content/*.mdx` → chunking → embeddings → Supabase → búsqueda semántica → contexto para Claude.
- Helper en `lib/rag.ts`.

**Vision (análisis de imágenes)**
- Para el UX Reviewer: enviar screenshots a Claude con `media_type: "image/jpeg"` en el content array.
- Limitar imágenes a 1MB antes de enviar; usar sharp para redimensionar si es necesario.

---

## Email

**Resend**
- Para el formulario de contacto y notificaciones.
- API Route en `app/api/contact/route.ts`.
- Variable requerida: `RESEND_API_KEY`.
- No usar nodemailer ni SMTP directamente.

---

## Pagos (Fase 4 — SaaS)

**Stripe**
- Checkout Sessions para planes del Design Critique Tool.
- Webhooks en `app/api/webhooks/stripe/route.ts`.
- Variables requeridas: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY`.

---

## Visualización de Datos

**Recharts**
- Para dashboards y gráficos simples dentro de proyectos de case study.
- Componentes wrapper en `components/charts/`.

**D3.js**
- Para visualizaciones custom que Recharts no puede manejar.
- Usar con `useEffect` y refs del DOM para no romper SSR.

---

## Testing

**Vitest**
- Tests unitarios para utilities en `lib/` y componentes puros.
- Configuración en `vitest.config.ts`. Correr con `npm run test`.

**Storybook**
- Documentación visual de componentes del design system.
- Stories en `*.stories.tsx` junto al componente.
- Correr con `npm run storybook`.

---

## Deploy & Infraestructura

**Vercel (Hobby)**
- Deploy automático desde rama `main`.
- Preview deployments en cada PR.
- Variables de entorno gestionadas desde el dashboard de Vercel, no en `.env` commiteado.
- El archivo `.vercel/project.json` está commiteado; contiene `projectId` y `orgId`.

**Límites del plan Hobby a respetar:**
- Serverless functions: timeout máximo de 10s (usar Edge Runtime para funciones de AI que streamen).
- Bandwidth: 100GB/mes (optimizar imágenes con Cloudinary).
- Sin teams: repositorio bajo cuenta personal.

---

## Variables de Entorno

Crear `.env.local` local con estas variables (nunca commitear):

```bash
# AI
ANTHROPIC_API_KEY=

# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Media
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

# Email
RESEND_API_KEY=

# Pagos (fase 4)
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=
```

---

## Convenciones Generales

- Componentes: PascalCase en `components/`.
- Utilities y helpers: camelCase en `lib/`.
- Tipos TypeScript en `types/` o co-localizados con el archivo que los usa.
- No usar `any`. Si el tipo es genuinamente desconocido, usar `unknown` y narrowing.
- Imports absolutos con alias `@/` (configurado en `tsconfig.json`).
- Antes de instalar un nuevo paquete, verificar si ya existe una solución en el stack actual.
