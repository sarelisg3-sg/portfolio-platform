# Handoff — ParkZone prototype/Figma fixes + roadmap next step

**Fecha:** 2026-07-08
**Sesión anterior:** `portfolio-platform/docs/handoffs/2026-07-07-P02-parkzone-case-study.md`
**Estado:** ParkZone (case study #3 de Portfolio V1) con 6 inconsistencias prototipo/Figma corregidas y desplegadas en producción · `portfolio-platform/projects.json` actualizado y pusheado

---

## Contexto de arranque

Esta sesión retomó desde el handoff del 2026-07-07 (`portfolio-platform/docs/handoffs/2026-07-07-P02-parkzone-case-study.md`), que dejó pendiente verificar visualmente el prototipo de ParkZone desplegado contra el diseño de Figma. La usuaria reportó 6 inconsistencias concretas (con screenshots) y se corrigieron todas.

---

## Cambios en `parkzone`

Repo: https://github.com/sarelisg3-sg/parkzone · Demo: https://parkzone-rho.vercel.app

| Commit | Qué hace |
|---|---|
| `ac7f69b` | Corrige 6 inconsistencias: botón "Cambiar" vehículo sin acción en Parámetros/Agregar tiempo; tarjeta sin acción y "Regresar" que rompía el flujo de pago en Métodos de pago/Pago; home no mostraba el auto estacionado tras pagar (ahora usa un hook `useRemainingTime` compartido y hay estado "Estacionamiento" dinámico); tooltip del parquímetro muy separado del pin; hamburger menu sin interacción y mal ubicado (ahora vive en `Header` con `onMenu`, abre `AccountMenu.tsx`, un drawer in-frame — no modal nativo, para no salirse del `PhoneFrame`) |
| `c95a95c` | El primer intento de arreglar el logo del splash/welcome fue a ojo (dasharray simétrico aproximado) y la usuaria lo rechazó comparando contra el HTML/CSS real que copió de Figma. Se resolvió encontrando que el **Dev Mode MCP Server de Figma seguía activo en `http://127.0.0.1:3845/mcp`** (igual que documenta el handoff anterior) — se usó `get_metadata`/`get_design_context` sobre el nodo `4049:164` ("logo") para sacar los dos SVG reales (`fae3781...svg` = ring, `84159e8...svg` = pin) y se copiaron los `<path>` exactos a `components/shell/Logo.tsx`. **Lección: si Figma Desktop con Dev Mode MCP Server está abierto, siempre preferir extraer el path SVG real antes que aproximar visualmente.** |
| `41d723c` | Fix de seguimiento: la usuaria detectó que la pantalla de home con sesión activa ("Estacionamiento") tenía el mismo bug del tooltip separado del pin que ya se había arreglado en la pantalla de selección de Parquímetro — quedó un `top-[46%]` viejo en vez de `top-[57%]` (mismo offset que el pin) en `HomeScreen` dentro de `components/screens/parking.tsx`. Corregido para que coincida con el patrón ya usado en `MeterDetectedScreen`. |

Todos los commits están pusheados a `main` y cada uno se verificó como deployment `READY` en Vercel (proyecto `prj_MVOjP6zhingEKn21sB9mHwfjdaXM`, team `team_Xmd5rC3xtFB3LhobmQXNgavT`) antes de darlo por cerrado.

### Cómo se accedió a Figma esta vez (actualización útil respecto al handoff anterior)

El handoff previo decía que `ToolSearch` no exponía las herramientas de Figma y que había que hablarle crudo al servidor Dev Mode MCP vía `curl`/`python3`. Esta sesión se confirmó que el servidor **seguía corriendo localmente** (`curl http://127.0.0.1:3845/mcp` responde). Flujo que funcionó:
1. `POST /mcp` con `method: initialize` → capturar el header `Mcp-Session-Id` de la respuesta.
2. `POST /mcp` con `notifications/initialized` (mismo session id).
3. `tools/call` → `get_metadata` sin `nodeId` para listar páginas top-level, luego con el `nodeId` de la página para encontrar el frame/nodo deseado (en este caso `welcome page` → `logo` → dos `icon logo`).
4. `tools/call` → `get_design_context` con el `nodeId` del grupo devuelve código React/Tailwind generado **más las URLs de los assets SVG/PNG reales** (`http://localhost:3845/assets/<hash>.svg`).
5. `curl` directo a esas URLs de assets descarga el SVG/PNG en resolución/fidelidad nativa — mucho mejor que reconstruir a mano.

Esto es más fiable que pedirle a la usuaria que copie/pegue el HTML CSS export de Figma (ese export aplana shapes compuestos a un `<div>` con `background` sólido sobre el bounding box, perdiendo la geometría real — no sirve para reconstruir paths).

---

## Cambios en `portfolio-platform`

Repo: https://github.com/sarelisg3-sg/portfolio-platform

| Commit | Qué hace |
|---|---|
| `6fe5918` | `projects.json`: marca `portfolio-v1` como `status: "done"` (`completed_at: 2026-07-07`), corrige `deployment` a `https://sarelisantiago.dev` (antes apuntaba a la URL de preview de Vercel), y agrega el array `case_studies` (Artium Online, Le Point du FLE, ParkZone) con sus repos/deploys. Esto cerraba un pendiente explícito del handoff del 2026-07-07 ("`projects.json` ... sigue reflejando el estado previo a este trabajo"). |

Queda sin trackear en este repo (no tocado, no es de esta sesión): `docs/handoffs/2026-07-06-P02-content-complete.md` — probablemente de una sesión anterior que no llegó a commitear ese handoff.

---

## Estado del roadmap (`portfolio-platform/docs/roadmap/roadmap-proyectos.md`)

Fase 1 — Fundamentos de Diseño & Frontend:

- ✅ **#1 Design System Personal** — done
- ✅ **#2 Portfolio V1** — done (3 case studies, dominio propio)
- ⬜ **#3 Landing con Animaciones** — siguiente sin empezar. **Importante:** es un proyecto/case-study nuevo e independiente (repo propio, se sugiere que el "producto imaginario" podría ser una landing promocional para el propio design system de P01), **no** es un rediseño del home de `portfolio-v1`. Stack: Next.js, Tailwind, Framer Motion, GSAP.
- ⬜ **#4 Rediseño de App Existente** — sin empezar. Pendiente de decidir si Le Point du FLE ya cubre el objetivo (research UX + prototipo Figma + implementación) o si conviene un proyecto nuevo desde cero.

---

## Pendientes que siguen abiertos (heredados del handoff anterior, no tocados esta sesión)

- La pantalla "Historial de pagos" de ParkZone (`HistorialScreen` en `parkzone/components/screens/account.tsx`) sigue usando 2 entradas mock ficticias porque el Figma original no tenía el diseño de alta fidelidad de esa pantalla. Si la usuaria consigue/crea ese diseño, valdría la pena ajustarla.
- No se ha corrido un `/code-review` formal sobre el repo `parkzone` (se construyó y se parcheó rápido en varias sesiones).

---

## Siguiente paso (lo que pidió la usuaria: "continuar con roadmap")

Arrancar **#3 Landing con Animaciones**. Sugerido:
1. Confirmar con la usuaria qué "producto imaginario" quiere usar de excusa (¿landing del propio design system? ¿algo distinto?).
2. Crear el repo nuevo (patrón similar a `parkzone`: copiar tokens/componentes de `design-system`, no modificar ese repo directamente).
3. Actualizar `portfolio-platform/projects.json` (`landing-animaciones`, actualmente `not-started`) cuando arranque.

---

## Suggested skills para la próxima sesión

- **`/to-issues`** — para convertir "Landing con Animaciones" en un issue formal de kickoff en `portfolio-platform`, siguiendo el patrón de los issues de kickoff que ya existen para P01/P02 (ver `kickoff_issue` en `projects.json`).
- **`/code-review`** — pendiente sobre el repo `parkzone` antes de darlo por completamente cerrado (ver sección de pendientes).
- **`/verify`** — para confirmar end-to-end en producción que los 3 fixes de esta sesión (menú, tooltip anclado, logo) se ven bien también en `https://parkzone-rho.vercel.app` directamente (esta sesión solo verificó contra el preview local antes de cada push, no releyó el sitio de producción después del deploy).
- **`/qa`** — si al arrancar la Landing con Animaciones se quiere una sesión de QA conversacional en vez de una revisión de código pura.
