# Roadmap de Proyectos — UI/UX · Frontend · AI Engineer

16 proyectos organizados en 4 fases progresivas. Cada proyecto está diseñado para ser un case study real en tu portfolio: tiene objetivo claro, stack definido y un entregable concreto que demuestra una habilidad específica.

---

## Fase 1 — Fundamentos de Diseño & Frontend
*Meses 1–3 · Base sólida de UI/UX + código*

El objetivo de esta fase es traducir lo que ya sabes de diseño a código real. Cada proyecto parte de algo conocido (Figma, diseño visual) y lo convierte en un producto funcionando en el browser.

---

### 1. Design System Personal

**Objetivo**
Construir tu propio sistema de diseño desde cero: desde los tokens hasta los componentes documentados. No es un ejercicio de copia — es definir tu voz visual y hacerla técnicamente reproducible.

**Qué incluye**
- Tokens de diseño: colores, tipografía, espaciado, radios, sombras
- Librería de componentes base: botones, inputs, cards, badges, modals
- Tema dark/light con variables CSS
- Documentación interactiva con Storybook

**Stack**
Figma (tokens) · Next.js · Tailwind CSS · shadcn/ui · Storybook

**Entregable**
Un Storybook publicado en Vercel con todos los componentes documentados y una guía de uso. Es el cimiento sobre el que construirás los proyectos siguientes.

**Por qué importa**
Demuestra que puedes pensar en sistemas, no solo en pantallas. Es el proyecto que más impresiona a equipos de producto porque muestra disciplina de diseñadora + habilidad técnica de frontend.

---

### 2. Portfolio V1

**Objetivo**
Lanzar tu primera versión del portfolio como desarrolladora. No tiene que ser perfecta — tiene que existir y estar en producción.

**Qué incluye**
- Homepage con presentación y selección de proyectos
- Case studies en MDX: contexto del problema, proceso, resultado
- Página de contacto con formulario funcional (Resend)
- Transiciones de página suaves con Framer Motion
- Metadata SEO y Open Graph configurados

**Stack**
Next.js · Tailwind CSS · MDX · Framer Motion · Resend · Vercel

**Entregable**
Portfolio en producción con al menos 3 case studies. URL propia (dominio custom conectado a Vercel).

**Por qué importa**
Es tu carta de presentación. Todo lo que construyas a partir de aquí vive aquí. También es la primera demostración pública de que puedes llevar un proyecto de diseño a producción completa.

---

### 3. Landing con Animaciones

**Objetivo**
Dominar animaciones de UI: scroll-triggered, micro-interactions y page transitions. La mayoría de los frontends evitan las animaciones porque son difíciles — tú las harás bien desde el principio.

**Qué incluye**
- Animaciones de entrada con scroll (stagger effects, parallax sutil)
- Micro-interactions en hover: botones, cards, navegación
- Hero animado con texto o elementos gráficos
- Transición entre secciones fluida
- Optimizado para 60fps (sin jank)

**Stack**
Next.js · Tailwind CSS · Framer Motion · GSAP (para scroll timeline)

**Entregable**
Landing page de un producto imaginario (puede ser para tu design system, una app ficticia, etc.) publicada en Vercel. El código debe estar limpio y reutilizable como patrón para futuros proyectos.

**Por qué importa**
Las animaciones bien hechas son un diferencial claro. Muy pocos juniors tienen esto sólido. Demuestra atención al detalle y comprensión de performance.

---

### 4. Rediseño de App Existente

**Objetivo**
Tomar una app real con problemas de usabilidad, hacer un proceso completo de UX research y entregar tanto el prototipo Figma como la implementación funcional.

**Qué incluye**
- Análisis heurístico de la app original
- Entrevistas o benchmarking documentado
- Wireframes y prototipo navegable en Figma
- Implementación en Next.js de al menos 3 pantallas clave
- Comparativa antes/después con métricas de mejora

**Stack**
Figma · Next.js · Tailwind CSS · shadcn/ui

**Entregable**
Case study completo: documento de proceso (puede ser en Notion o MDX) + prototipo Figma + implementación funcional en Vercel.

**Por qué importa**
Es el proyecto que más habla de tu proceso de diseño. Combina research, diseño y código — exactamente el perfil de una product designer que también programa.

---

## Fase 2 — Interactividad & Datos
*Meses 4–6 · Apps con estado, APIs y visualización*

En esta fase dejas de construir páginas estáticas y empiezas a construir aplicaciones reales: con datos, estado compartido, interacciones complejas y lógica de negocio.

---

### 5. Dashboard de Analytics

**Objetivo**
Construir un dashboard interactivo que consuma datos reales (o semi-reales) y los visualice de forma comprensible. El reto no es solo mostrar números — es diseñar la información para que sea accionable.

**Qué incluye**
- Conexión a una API pública (GitHub, OpenWeather, o datos propios en Supabase)
- Gráficos interactivos: líneas, barras, áreas, donut charts
- Filtros de rango de tiempo
- Tabla de datos con ordenamiento y paginación
- Estado de carga y manejo de errores

**Stack**
Next.js · Recharts · Supabase (o API pública) · Tailwind CSS · shadcn/ui

**Entregable**
Dashboard publicado en Vercel con datos reales actualizándose. Documentado como case study con decisiones de diseño de información.

**Por qué importa**
La visualización de datos es una habilidad muy buscada. Combina diseño (jerarquía de información) con frontend (performance con grandes datasets). Diferencia a una frontend de las demás.

---

### 6. E-commerce UI

**Objetivo**
Construir la UI completa de una tienda: desde el catálogo hasta el checkout. El foco está en el UX del flujo de compra — uno de los flows más críticos que existen en producto.

**Qué incluye**
- Catálogo con filtros, búsqueda y ordenamiento
- Página de producto con galería de imágenes
- Carrito con estado persistente (localStorage)
- Checkout multi-step con validación de formularios
- Estados vacíos, loading y error bien diseñados

**Stack**
Next.js · Tailwind CSS · Zustand (estado global del carrito) · shadcn/ui

**Entregable**
E-commerce funcional publicado en Vercel. El carrito debe persistir entre sesiones. Case study documentando las decisiones UX del checkout.

**Por qué importa**
El e-commerce es uno de los dominios más estudiados en UX. Tener uno implementado demuestra que entiendes flows complejos con múltiples estados y errores.

---

### 7. App Colaborativa en Tiempo Real

**Objetivo**
Construir una app donde múltiples usuarios puedan ver e interactuar al mismo tiempo. Introducción a real-time y presencia de usuarios — tecnología que está en Figma, Notion, Linear y todas las apps modernas.

**Qué incluye**
- Lista o tablero compartido que se sincroniza entre pestañas/dispositivos
- Indicadores de presencia: "3 personas viendo esto ahora"
- Actualizaciones en tiempo real sin recargar la página
- Cursores o avatares de usuarios conectados (opcional)

**Stack**
Next.js · Supabase Realtime · Tailwind CSS · Framer Motion

**Entregable**
App funcional donde abrir dos pestañas demuestra la sincronización en vivo. Puede ser un tablero de ideas, una lista de tareas compartida, o un canvas colaborativo simple.

**Por qué importa**
Las apps en tiempo real son técnicamente complejas. Construir una demuestra que entiendes WebSockets y arquitectura de datos reactiva — habilidades de nivel senior que pocos juniors tienen.

---

### 8. Component Library Pública

**Objetivo**
Publicar tu design system como un paquete npm real que cualquiera pueda instalar. Es la versión productizada del Proyecto 1.

**Qué incluye**
- Componentes exportados como paquete npm
- TypeScript completo con tipos exportados
- Documentación con Storybook publicado
- Tests de accesibilidad (a11y) con axe-core
- README con guía de instalación y uso

**Stack**
React · TypeScript · Tailwind CSS · Storybook · Vitest · npm

**Entregable**
Paquete publicado en npm con al menos 10 componentes. Storybook publicado en Vercel. README completo en GitHub.

**Por qué importa**
Publicar en npm es un hito. Demuestra que tu trabajo es lo suficientemente maduro para que otros lo usen. Es la prueba más concreta de calidad de código.

---

## Fase 3 — AI Integration
*Meses 7–9 · Conectar LLMs a productos reales*

Aquí empieza el diferencial real. No es usar ChatGPT — es integrar modelos de lenguaje en productos con UX bien pensada. El foco está en hacer la AI útil, no en hacerla visible.

---

### 9. Chat UI con Streaming

**Objetivo**
Construir una interfaz de chat con un LLM que tenga streaming real, markdown renderizado, historial de conversación y manejo correcto de estados (cargando, error, éxito).

**Qué incluye**
- Input con envío por Enter y botón
- Respuestas que aparecen token a token (streaming)
- Markdown renderizado: código, listas, negritas, links
- Historial scrolleable con diferenciación visual usuario/AI
- Botón de "detener generación"
- Estado de error con opción de reintentar

**Stack**
Next.js · Vercel AI SDK · Claude API (Anthropic) · Tailwind CSS · react-markdown

**Entregable**
Chat funcional publicado en Vercel. El streaming debe verse fluido. Puede tener un sistema prompt que lo especialice en un tema (diseño, francés, código, etc.).

**Por qué importa**
El chat es el patrón de UI más común en productos AI. Dominarlo bien — con streaming, estados y UX pulida — es la base de casi todo lo que viene en Fase 4.

---

### 10. AI Design Token Generator

**Objetivo**
Construir una herramienta que tome un brief de diseño en texto y genere automáticamente una paleta de colores, tipografía sugerida y tokens de espaciado coherentes.

**Qué incluye**
- Input de brief: "Una app de finanzas seria y confiable para adultos mayores"
- Output: paleta de colores con hex codes y nombres
- Sugerencias de tipografía con justificación
- Escala de espaciado y radios sugeridos
- Preview visual de los tokens generados
- Botón de exportar como CSS variables o JSON

**Stack**
Next.js · Claude API · Tailwind CSS · Framer Motion (para el reveal de resultados)

**Entregable**
Herramienta pública donde cualquier diseñador puede ingresar un brief y obtener una propuesta de tokens en segundos. Publicada en Vercel.

**Por qué importa**
Es una herramienta que tú misma usarías. Combina tu expertise en diseño (sabes qué es un token bien hecho) con AI. Proyectos así se viralizan en comunidades de diseño.

---

### 11. UX Reviewer con AI

**Objetivo**
Construir una herramienta que tome un screenshot de una interfaz y entregue feedback de usabilidad estructurado: qué funciona, qué no, y por qué.

**Qué incluye**
- Upload de imagen (screenshot de cualquier app o diseño)
- Análisis de la imagen con Claude Vision
- Feedback estructurado en categorías: jerarquía visual, accesibilidad, claridad, consistencia
- Nivel de severidad por issue (crítico, importante, sugerencia)
- Posibilidad de hacer preguntas de seguimiento sobre el diseño

**Stack**
Next.js · Claude API (Vision) · Tailwind CSS · shadcn/ui

**Entregable**
Herramienta publicada donde cualquiera puede subir una captura de pantalla y recibir un análisis de UX en 10 segundos. Incluye ejemplos pre-cargados para demostración.

**Por qué importa**
Demuestra que puedes pensar en cómo la AI aumenta el trabajo de diseño en lugar de reemplazarlo. Es un caso de uso concreto, útil, y que solo alguien con expertise en UX podría construir bien.

---

### 12. AI Copy Generator para UI

**Objetivo**
Construir una herramienta que genere microcopy de interfaz: textos de botones, mensajes de error, estados vacíos, tooltips, onboarding — todo el texto pequeño que hace o rompe un producto.

**Qué incluye**
- Selección de tipo de copy: botón, error, vacío, onboarding, notificación
- Input de contexto: qué hace el producto, tono, público
- Generación de 3 variantes por solicitud
- Opción de ajustar tono: formal, amigable, técnico, urgente
- Historial de lo generado en la sesión

**Stack**
Next.js · Claude API · Tailwind CSS

**Entregable**
Herramienta publicada en Vercel con al menos 6 tipos de copy soportados. Incluye ejemplos de output en el landing.

**Por qué importa**
El microcopy es una de las áreas más descuidadas del diseño y una de las que más impacto tiene en conversión. Una herramienta así es práctica, tiene audiencia real, y demuestra comprensión de product writing.

---

## Fase 4 — AI Nativa — Productos Propios
*Meses 10–12 · Productos donde la AI es el núcleo, no un feature*

En esta fase la AI no es una función adicional — es la razón de ser del producto. El objetivo es construir cosas que no podrían existir sin LLMs.

---

### 13. Portfolio V2 con AI

**Objetivo**
Evolucionar tu portfolio para que sea interactivo: un chatbot que conoce tu trabajo y puede responder preguntas sobre él, más búsqueda semántica entre proyectos.

**Qué incluye**
- Chatbot entrenado sobre tus case studies, skills y experiencia
- Búsqueda semántica: "muéstrame proyectos donde usé Figma con real-time"
- Embeddings de todo el contenido del portfolio (MDX + textos)
- Respuestas con citas y links a los proyectos relevantes
- UI de chat integrada de forma no intrusiva en el diseño del portfolio

**Stack**
Next.js · Claude API · Vercel AI SDK · Supabase + pgvector (RAG) · Embeddings · MDX

**Entregable**
Portfolio publicado donde un reclutador puede preguntarle directamente a tu portfolio "¿Tiene experiencia con diseño de sistemas?" y recibir una respuesta fundamentada con ejemplos.

**Por qué importa**
Es el proyecto que más abre conversaciones en entrevistas. Nadie más lo tiene. Demuestra que entiendes RAG, embeddings y cómo hacer AI útil en un contexto de producto real.

---

### 14. Design Critique Tool (SaaS)

**Objetivo**
Evolucionar el UX Reviewer (Proyecto 11) a un producto SaaS con usuarios reales, planes y pagos.

**Qué incluye**
- Landing page con propuesta de valor clara
- Autenticación con magic link (Supabase Auth)
- Plan gratuito: 5 análisis/mes · Plan Pro: ilimitado
- Historial de análisis guardados por usuario
- Exportar análisis como PDF
- Checkout con Stripe

**Stack**
Next.js · Claude API (Vision) · Supabase (auth + DB) · Stripe · Resend · Tailwind CSS

**Entregable**
Producto funcional con al menos 2 planes, checkout real y usuarios reales (aunque sean conocidos). Métricas de uso en dashboard interno.

**Por qué importa**
Tener un SaaS propio es el proyecto más serio que puedes mostrar. Demuestra que puedes llevar un producto completo: diseño, desarrollo, pagos, auth, y que entiendes el negocio detrás del código.

---

### 15. UI Generator desde Prompts

**Objetivo**
Construir una herramienta que tome una descripción en texto y genere componentes React renderizados en vivo que el usuario puede editar y exportar.

**Qué incluye**
- Input de texto: "Un card de producto con imagen, título, precio y botón de agregar al carrito"
- Generación de código JSX con Tailwind
- Preview en vivo del componente renderizado
- Editor de código editable (monaco-editor o CodeMirror)
- Exportar como archivo .tsx
- Historial de componentes generados en la sesión

**Stack**
Next.js · Claude API · Sandpack (para ejecución segura de código generado) · Monaco Editor · Tailwind CSS

**Entregable**
Herramienta publicada donde en 30 segundos puedes ir de una descripción en español a un componente React listo para copiar.

**Por qué importa**
Es la intersección más visible de diseño + código + AI. Es el tipo de herramienta que sale en Twitter. Demuestra comprensión profunda de code generation y sandboxing seguro.

---

### 16. AI Design System Docs

**Objetivo**
Construir la documentación de tu design system (Proyecto 1 y 8) que responde preguntas: en lugar de buscar en la docs, le preguntas directamente.

**Qué incluye**
- Ingestión de toda la documentación del design system (MDX, código, Storybook)
- Chat que responde preguntas: "¿Cuándo uso un modal vs un drawer?"
- Búsqueda semántica entre componentes
- Respuestas que incluyen el código de uso correcto
- Sincronización automática cuando la docs cambia (webhook o cron)

**Stack**
Next.js · Claude API · Vercel AI SDK · Supabase + pgvector · MDX · Embeddings

**Entregable**
Documentación de tu design system con chat integrado, publicada en Vercel. Cualquier developer puede preguntarle cómo usar un componente y recibe una respuesta con código de ejemplo.

**Por qué importa**
Cierra el círculo del roadmap: comenzaste construyendo un design system, y terminas haciendo que ese design system sea inteligente. Es la demostración más madura de que combinas diseño de sistemas, frontend y AI en un solo flujo.

---

## Resumen

| Fase | Proyectos | Habilidad principal |
|---|---|---|
| 1 — Fundamentos | Design System, Portfolio V1, Landing animada, Rediseño | Diseño → Código |
| 2 — Interactividad | Dashboard, E-commerce, Real-time, npm package | Apps complejas con datos |
| 3 — AI Integration | Chat UI, Token Generator, UX Reviewer, Copy Generator | LLMs como feature |
| 4 — AI Nativa | Portfolio V2, SaaS, UI Generator, Docs con AI | AI como producto |

**Tiempo estimado:** 12 meses a ritmo sostenible (1 proyecto cada 3 semanas).
**Inversión:** $0 en infraestructura durante el desarrollo (todo corre en capas gratuitas).
**Resultado:** 16 proyectos deployados, un portfolio con case studies reales, y un perfil que combina diseño + frontend + AI de forma creíble y demostrable.
