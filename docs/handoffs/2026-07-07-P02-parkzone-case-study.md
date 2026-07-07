# Handoff — Portfolio V1 fixes + ParkZone case study #3

**Fecha:** 2026-07-07
**Sesión anterior:** `portfolio-platform/docs/handoffs/2026-07-06-P02-content-complete.md`
**Estado:** Portfolio V1 completo con 3 case studies · Todo commiteado, CI verde, desplegado en producción

---

## Contexto de arranque

Esta sesión retomó desde el handoff del 2026-07-06. Se resolvieron todos los pendientes marcados ahí (Resend key, cleanup de `le-point-du-fle-next`, verificación de la foto del hero) y se construyó un tercer case study completo (ParkZone) a partir de una presentación PPTX y un prototipo de Figma reales de la usuaria.

---

## Cambios en `portfolio-v1`

Repo: https://github.com/sarelisg3-sg/portfolio-v1 · Producción: https://sarelisantiago.dev

| Commit | Qué hace |
|---|---|
| `76ee7b3` | Corrige que el francés aparecía como lengua materna (es C2, no nativo) en los 3 idiomas; rebalancea hero/about hacia herramientas antes que idiomas |
| `77ab321` | `ProjectCard` ahora usa patrón stretched-link (toda la card es clickeable al detalle, "Ver sitio" sigue yendo directo al externo); expone el case study de Artium Online (antes oculto por `type: external`); corrige Le Point du FLE para apuntar al prototipo HTML completo y validado en vez del rediseño Next.js incompleto (que se borró, ver abajo) |
| `2b7fdc2` | Menú hamburguesa en mobile — el navbar no tenía fallback responsive y se encimaba en pantallas ~375px |
| `e7aa8f5` | Añade case study de ParkZone (es/en/fr) — 3er proyecto destacado |
| `d72d42c`/`a06b73f` (en `parkzone` y aquí) | Reemplaza el mapa pixeleado por la fuente en resolución nativa (ver sección ParkZone) |

**`le-point-du-fle-next` fue eliminado por completo** (repo GitHub, proyecto Vercel, carpeta local) — era una reimplementación Next.js incompleta y confusa; `le-point-du-fle` (el prototipo HTML estático completo y validado con usuarios) es el que se conserva y al que apunta el portfolio. También se limpió la referencia obsoleta en `portfolio-platform/README.md`.

**Resend API key:** la usuaria confirmó que ya revocó la key original (compartida por accidente en el chat) y configuró una nueva en Vercel. Resuelto, no requiere seguimiento.

---

## Proyecto nuevo: ParkZone (case study #3)

**Repo:** https://github.com/sarelisg3-sg/parkzone (público) · **Demo:** https://parkzone-rho.vercel.app

Reconstrucción completa en código del prototipo Figma de la usuaria — una app de parquímetros para CDMX, proyecto final de UX con research, card sorting, evaluación heurística y pruebas de usabilidad con 5 usuarios (datos reales: 127s promedio, 4.2/5 satisfacción). El plan completo de esta construcción está en `/Users/sarelisantiagogarcia/.claude/plans/linear-doodling-star.md`.

### Decisiones clave (no repetir el trabajo de descubrirlas)

- **El repo `design-system` (P01) nunca se modifica.** Se copió su arquitectura (tokens `--ds-*`, componentes Button/Card/Modal/Badge/Input/Typography, patrón cva + `cn()`) dentro de `parkzone/`, y solo ahí se recalculó la escala de marca de violeta a teal (oklch hue 208, calibrado para que brand-400≈`#48a5ad` y brand-800≈`#104d5f`, los colores reales extraídos del código generado por Figma).
- **Se construyó el prototipo completo (~39 pantallas)**, no solo el flujo validado con usuarios — la usuaria lo pidió explícitamente tras preguntarle. Incluye onboarding completo (login, olvidé contraseña, crear cuenta en 4 pasos con stepper) además del flujo de estacionamiento y gestión de cuenta.
- **Presentación:** marco de iPhone centrado (390×844 exacto, escala uniforme vía `PhoneFrame.tsx`) en vez de reinterpretar como sitio responsive — es fiel a que es una app, no un sitio web, a diferencia de los otros 2 proyectos del portfolio.
- **El mapa de fondo es Google Maps real** (un "Map Maker" screenshot que la usuaria pegó en su Figma, con atribución "Map data ©2024 Google, INEGI" visible) — no hace falta integrar una API de mapas.

### Cómo se accedió a Figma (útil si hace falta de nuevo)

`ToolSearch` nunca expuso las herramientas reales de Figma (`get_design_context`, `get_screenshot`, `get_metadata`) en esta sesión — solo `read_skill_uri`. La app de escritorio de Figma, con el archivo abierto y el **Dev Mode MCP Server activado** (Figma → Preferences → Enable Dev Mode MCP Server), expone un servidor local en `http://127.0.0.1:3845/mcp`. Se le habló directo por HTTP/JSON-RPC crudo vía `curl`/`python3` (no por ToolSearch) — ver `initialize` → `notifications/initialized` → `tools/call` con `get_screenshot`/`get_metadata`/`get_design_context`. El script usado está en el scratchpad de esta sesión (ver más abajo, puede no persistir).

**Los assets de imagen embebidos en Figma se pueden descargar en resolución nativa** desde `http://localhost:3845/assets/<hash>.png`, referenciados en la salida de `get_design_context` — mucho mejor que recortar un `get_screenshot` (que renderiza a la escala del frame, no a resolución nativa). Así se resolvió el pixeleo del mapa.

### Pendiente / no verificado

- La usuaria no ha dado confirmación visual final del fix del marco 390×844 ni del mapa nítido — el último mensaje del chat fue justo después de reportar CI verde en ambos repos. Vale la pena preguntar si ya lo vio bien antes de dar por cerrado el tema.
- La pantalla "Historial de pagos" en Figma solo tenía el botón de entrada, no una pantalla de lista de alta fidelidad — se construyó `HistorialScreen` con datos mock (la sesión real + 2 entradas ficticias). Si la usuaria tiene el diseño real de esa pantalla, valdría la pena ajustarla.
- Los screenshots de Figma capturados esta sesión (`figma_screens/*.png`, ~40 archivos) y el script `fig_screenshot.py` viven en el scratchpad de la sesión anterior — **probablemente no persisten** a una sesión nueva. Si se necesitan de nuevo, re-capturar desde Figma (Dev Mode MCP Server debe seguir activo y el archivo abierto).

---

## Estado del roadmap (`portfolio-platform/docs/roadmap/roadmap-proyectos.md`)

Portfolio V1 (P02) ahora cumple el mínimo de 3 case studies del roadmap. Siguientes proyectos de la Fase 1 sin empezar: **#3 Landing con Animaciones** y **#4 Rediseño de App Existente** (nota: Le Point du FLE ya cubre buena parte de lo que pediría el #4 — vale la pena decidir si cuenta o se hace uno nuevo).

`projects.json` en `portfolio-platform` no se actualizó esta sesión — sigue reflejando el estado previo a este trabajo.

---

## Suggested skills para la próxima sesión

- **`/verify`** — para que la usuaria (o un agente) confirme end-to-end que el demo de ParkZone funciona en producción tal cual se probó en preview.
- **`/qa`** — para revisar las 3 pantallas del case study de ParkZone en los 3 idiomas y detectar cualquier detalle suelto.
- **`/code-review`** — antes de dar por "terminado" el repo `parkzone`, una pasada de revisión de código no estaría de más (se construyó rápido, en una sola sesión, sin review).
- **`/to-issues`** — si se quiere convertir "Landing con Animaciones" / "Rediseño de App" en issues formales del roadmap para arrancar la siguiente fase.
