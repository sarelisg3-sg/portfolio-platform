# PRD-001: Portfolio Platform — UI/UX · Frontend · AI Engineer

**Status:** Ready for agent  
**Published:** 2026-06-17  
**GitHub Issue:** https://github.com/sarelisg3-sg/portfolio-platform/issues/1

---

## Problem Statement

Una diseñadora en transición a UI/UX + Frontend + AI Engineering tiene instinto visual sólido y proceso de diseño documentado, pero ningún portfolio técnico público que demuestre habilidades de frontend y AI a equipos de hiring. Existen proyectos experimentales aislados (todo-app, conversión Next.js de le-point-du-fle) pero no forman una narrativa coherente. Los recruiters y hiring managers que evalúan perfiles de product designer + engineer necesitan ver credibilidad técnica progresiva — un arco claro de diseño-a-código a productos AI-nativos — respaldada por software desplegado y funcionando.

Sin esto, la transición a un rol híbrido diseñadora/engineer queda indocumentada: las habilidades existen en teoría pero no en evidencia.

## Solution

Construir una plataforma de portfolio estructurada de 16 proyectos desplegados en 12 meses, organizados en 4 fases progresivas, todos en Vercel Hobby (costo de infraestructura: $0). Cada proyecto es un case study independiente con objetivo, stack y entregable definidos. La plataforma culmina en Portfolio V2 — un portfolio con AI donde los recruiters pueden hacer preguntas y recibir respuestas fundamentadas y citadas sobre habilidades y experiencia.

**Las 4 fases:**
- **Fase 1 — Diseño & Frontend Fundamentals** (meses 1–3): Design System Personal, Portfolio V1, Landing con Animaciones, Rediseño de App
- **Fase 2 — Interactividad & Datos** (meses 4–6): Dashboard de Analytics, E-commerce UI, App Colaborativa Real-time, Component Library pública (npm)
- **Fase 3 — AI Integration** (meses 7–9): Chat UI con Streaming, AI Design Token Generator, UX Reviewer con AI, AI Copy Generator
- **Fase 4 — AI Nativa** (meses 10–12): Portfolio V2 con AI, Design Critique SaaS, UI Generator desde Prompts, AI Design System Docs

## User Stories

**Como builder (Sareli):**
1. As the portfolio builder, I want a personal design system with documented tokens and components in Storybook, so that I can demonstrate systems thinking to hiring teams.
2. As the portfolio builder, I want to publish my design system as an npm package, so that I can show my work is production-quality and usable by others.
3. As the portfolio builder, I want case studies written in MDX with frontmatter metadata, so that each project has a documented process narrative alongside working code.
4. As the portfolio builder, I want a Portfolio V1 in production with a custom domain, so that I have a public professional presence from month 2 onward.
5. As the portfolio builder, I want animated UI with GSAP scroll timelines and Framer Motion micro-interactions, so that I can demonstrate performance-conscious animation that few juniors can match.
6. As the portfolio builder, I want an app redesign case study with a before/after comparison and UX metrics, so that I can show my full design process: heuristic analysis, wireframes, prototyping, implementation.
7. As the portfolio builder, I want a real-time collaborative app built on Supabase Realtime, so that I can demonstrate WebSocket architecture and reactive data patterns.
8. As the portfolio builder, I want a streaming chat UI with Claude, so that I have mastery of the AI UX pattern most common in production products.
9. As the portfolio builder, I want an AI tool that generates design tokens from a text brief, so that I can demonstrate domain-expert use of LLMs — only someone who knows tokens can make this useful.
10. As the portfolio builder, I want a UX Reviewer tool powered by Claude Vision, so that I can show AI as a design augmentation tool rather than a replacement.
11. As the portfolio builder, I want an AI Copy Generator for UI microcopy, so that I can demonstrate product writing expertise combined with AI generation.
12. As the portfolio builder, I want a SaaS product (Design Critique Tool) with Stripe, Supabase Auth, and usage limits, so that I can show I can ship a complete product end-to-end including payments and auth.
13. As the portfolio builder, I want a UI Generator that renders JSX from text prompts in a live sandbox, so that I can demonstrate code generation, sandboxing, and the intersection of design + AI.
14. As the portfolio builder, I want Portfolio V2 to answer recruiter questions about my work using RAG over my case studies, so that the portfolio itself is the strongest demo of my AI engineering skills.
15. As the portfolio builder, I want design system documentation with an embedded chat interface, so that I close the arc: I built a system, then made it intelligent.
16. As the portfolio builder, I want every project deployed independently to Vercel Hobby, so that each case study has its own live URL to link from the portfolio.
17. As the portfolio builder, I want all projects to stay within $0 infrastructure cost during development, so that I can build the full platform without upfront investment.

**Como recruiter / hiring manager:**
18. As a recruiter, I want to browse a portfolio organized by skill category, so that I can quickly assess if the candidate matches the role's requirements.
19. As a recruiter, I want to ask Portfolio V2 a direct question ("Does she have Figma + realtime experience?"), so that I can evaluate fit without reading every case study.
20. As a recruiter, I want Portfolio V2 to cite specific projects when answering questions, so that I can verify the claims myself.
21. As a hiring manager on a product team, I want to see a deployed Storybook with documented components, so that I know the candidate thinks in systems, not just screens.
22. As a hiring manager on an AI product team, I want to see at least one tool where AI is the core product (not a feature), so that I know the candidate understands AI product design.
23. As a hiring manager, I want case studies with documented design decisions and metrics, so that I can evaluate the candidate's design process, not just visual output.
24. As a recruiter, I want portfolio pages to load fast and have correct SEO metadata and Open Graph tags, so that I can share links that preview correctly in Slack or email.

**Como visitante / diseñador par:**
25. As a peer designer visiting the portfolio, I want to try the AI Design Token Generator with my own brief, so that I understand immediately what the tool does.
26. As a peer designer, I want to upload a screenshot to the UX Reviewer and get instant structured feedback, so that I can evaluate the tool's usefulness for my own work.
27. As a developer visiting the npm package documentation, I want a clear README with installation instructions and usage examples, so that I can integrate the component library in minutes.
28. As a visitor, I want to see an animated landing page that loads at 60fps with no layout shift, so that the technical quality is apparent from the first second.
29. As a visitor, I want an e-commerce UI with a persistent cart across sessions, so that I experience a complete, production-like purchase flow.

**Como consumidor open-source del npm package:**
30. As a developer installing the npm package, I want TypeScript types exported alongside components, so that I have autocomplete and type safety in my editor.
31. As a developer, I want the component library to pass axe-core accessibility checks, so that I can use it in products with accessibility requirements.
32. As a developer, I want Storybook to be publicly accessible on Vercel, so that I can evaluate components without installing the package.

**Como usuario del SaaS (Design Critique Tool):**
33. As a free plan user, I want 5 AI analysis credits per month, so that I can evaluate the tool before committing to a paid plan.
34. As a pro plan user, I want unlimited analyses and a history of past reviews, so that I can use the tool as part of my regular design workflow.
35. As a pro plan user, I want to export any analysis as a PDF, so that I can share it with my team or include it in design documentation.

## Implementation Decisions

### Framework & Routing
- Exclusivamente Next.js 16+ App Router (`app/` directory). Sin `pages/` router.
- Server Components por defecto. `"use client"` solo cuando se necesita estado de browser o eventos.
- Rutas dinámicas para proyectos: `app/projects/[slug]/page.tsx`.
- API Routes en `app/api/` para todos los endpoints de AI y formularios.
- Las llamadas a Claude API van SIEMPRE desde Server Components o API Routes — nunca se expone la API key al cliente.

### Design System (Proyectos 1 y 8)
- Tokens de diseño definidos en Figma y reflejados como CSS custom properties en `app/globals.css`.
- La component library se construye como paquete npm independiente con TypeScript types exportados.
- Storybook desplegado a Vercel para documentación pública.
- Componentes shadcn/ui en `components/ui/` — se extienden pero nunca se modifican directamente.

### Estilos
- Tailwind CSS v4 con clases utilitarias en JSX.
- Sin CSS Modules salvo excepciones justificadas (ej. keyframes complejos).
- Inline styles solo donde fidelidad pixel-perfect al diseño original lo requiere.

### Animaciones
- Framer Motion para animaciones a nivel de componente (entrada, salida, micro-interactions). Variants centralizados en `lib/animations.ts`.
- GSAP + `@gsap/react` `useGSAP()` para timelines de scroll. No se mezcla con Framer Motion sobre el mismo elemento.
- Target de performance: 60fps, sin layout shift.

### Contenido & MDX
- Case studies en `content/projects/*.mdx` con frontmatter YAML: `title`, `date`, `tags`, `cover`, `summary`.
- Procesado con `next-mdx-remote` o `@next/mdx`. Custom MDX components registrados en `lib/mdx-components.tsx`.

### Media
- `<Image>` de `next/image` para todas las imágenes del proyecto. Nunca `<img>` directo.
- Cloudinary para imágenes de alta resolución. Transformaciones vía `lib/cloudinary.ts`.

### Capa AI
- Modelos: `claude-haiku-4-5-20251001` para respuestas rápidas, `claude-sonnet-4-6` para análisis complejos (UX Review, RAG retrieval).
- Streaming vía Vercel AI SDK `streamText()` con `@ai-sdk/anthropic`.
- `useChat()` para interfaces de chat, `useCompletion()` para generaciones one-shot.
- Route handlers: `app/api/chat/route.ts`, `app/api/completion/route.ts`.
- Vision: screenshots enviados a Claude como base64 con `media_type: "image/jpeg"`, redimensionados a < 1MB con sharp antes de enviar.

### RAG Pipeline (Proyectos 13 y 16)
- Contenido de `content/*.mdx` → chunking → embeddings → Supabase con pgvector.
- Modelo de embeddings: OpenAI `text-embedding-3-small` o equivalente Cohere.
- Helper de retrieval en `lib/rag.ts`. Lógica pura de retrieval separada de las llamadas al proveedor para testabilidad.
- Las respuestas incluyen citas con links a los proyectos fuente.

### Real-time (Proyecto 7)
- Supabase Realtime vía `supabase.channel()` para presencia y sincronización.
- Sin polling — modelo puro de eventos WebSocket.

### Estado Global
- Zustand para estado del carrito en el proyecto e-commerce. Sin Redux.
- Persistencia del carrito vía localStorage.
- Todo otro estado: React `useState`/`useReducer` a nivel de componente.

### Auth & Pagos (Proyecto 14 — SaaS)
- Supabase Auth con magic link (sin auth de contraseña).
- Stripe Checkout Sessions para upgrades de plan.
- Webhooks en `app/api/webhooks/stripe/route.ts`.
- Límites de uso aplicados server-side contra registros de quota en Supabase.

### Email
- Resend para formulario de contacto y email transaccional. Sin SMTP.
- Route handler en `app/api/contact/route.ts`.

### UI Generator Sandbox (Proyecto 15)
- Sandpack para ejecución segura de JSX generado por AI en iframe aislado.
- Monaco Editor o CodeMirror para la vista de código editable.
- Output exportado como archivo `.tsx`.

### Deploy
- Todos los proyectos nuevos usan GitHub-first deploy: git push → CI → Vercel auto-deploy.
- Variables de entorno gestionadas desde el dashboard de Vercel, nunca commiteadas.
- Límites de Vercel Hobby respetados: timeout de serverless functions ≤ 10s (usar Edge Runtime para rutas de AI con streaming).

### Convenciones
- Componentes: PascalCase en `components/`.
- Utilities y helpers: camelCase en `lib/`.
- Tipos TypeScript en `types/` o co-localizados.
- Sin `any`. Tipos genuinamente desconocidos usan `unknown` con narrowing.
- Imports absolutos via alias `@/`.

## Testing Decisions

Ver [ADR-003: Testing Seams](../adr/ADR-003-testing-seams.md) para la decisión completa.

Un buen test verifica comportamiento externo — qué produce el módulo dado un input específico — no detalles de implementación, estado interno, ni qué funciones fueron llamadas internamente.

### Seam 1: `lib/` utilities → Vitest unit tests
Funciones puras y lógica determinista. Para módulos con proveedores externos: separar lógica pura de la llamada al proveedor y testear solo la capa pura.

### Seam 2: Components → Storybook + axe-core + Testing Library
Stories para variantes visuales, axe-core para a11y automática, Testing Library para componentes interactivos (afirmando sobre output visible, no estado interno).

### Seam 3: API Routes → integration tests contra route handlers reales
Route handlers con requests/responses realistas. Lógica principal sin mockear. Servicios externos controlables con test mode, fixtures o mocks seguros.

### Seam 4: npm package → CI gate antes de publish
`typecheck → lint → build → Vitest → selected snapshots → Storybook build → axe-core`. Pipeline bloqueante. Snapshots como señal de detección, no árbitro.

## Out of Scope

- GitHub integration automática en proyectos existentes (migrar cuando aplique, no bloquear)
- CMS de terceros (Contentful, Sanity)
- Apps móviles (React Native)
- i18n / routing multi-idioma
- Tests E2E con Playwright o Cypress
- Monorepo (ver ADR-001)
- Infraestructura backend más allá de Supabase

## Further Notes

- **Límites de Vercel Hobby son una restricción dura**: timeout ≤ 10s, 100GB bandwidth/mes. Rutas de AI con streaming deben usar Edge Runtime.
- **El orden de los proyectos importa**: P8 productiza P1; P11 evoluciona a P14; P16 depende de P1, P8 y P13. Construir fuera de orden genera retrabajo.
- **La restricción de $0** es real e intencional para todo el período de desarrollo.
- **Ritmo**: un proyecto cada 3 semanas. 16 × 3 = 48 semanas ≈ 12 meses.
- **`AGENTS.md`** en este repositorio es la referencia autoritativa del stack. Mantenerlo actualizado a medida que las decisiones evolucionan.
