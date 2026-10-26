# AGENTS.md — Instrucciones para agentes IA

> Este archivo es auto-contenido. No necesitas leer nada más para trabajar.
> Si hay conflicto con otro archivo, este manda en proceso; en criterio
> de producto manda `specs/constitution.md`.

## Proyecto
Esqueleto mínimo para desarrollo de software con IA. Ejemplo de referencia
con estructura Next.js 14 (App Router). Sin app real todavía, solo plantillas.

## Stack tecnológico
- Next.js 16 con React 19 + TypeScript estricto.
- Vite como entorno de desarrollo, Tailwind CSS para estilos, Node 24 LTS y npm como gestor.
- GitHub Actions para CI. Prettier + ESLint para formato y lint.

## Estructura del proyecto
- `app/` rutas, layouts y páginas. Server Components por defecto.
- `components/` componentes UI reutilizables.
- `lib/` lógica de negocio, helpers y acceso a datos.
- `public/` archivos estáticos.
- `docs/` documentación del proyecto.
- `AGENTS.md` reglas del agente. `MEMORY.md` memoria del proyecto.
- `.opencode/commands/` familia `/sdd/*` (9 en `sdd/`: constitution, spec, clarify, plan, tasks, implement, validate, change, status) + `/publicar-git`, `/nuevo-componente`.
- `.opencode/skills/` skills `sdd`, `publicar-git`, `nextjs-patterns`, `tailwind-estilos`, `actualizar-memoria`.
- `.opencode/agents/` subagentes SDD: coordinador, planner, implementer, reviewer. Ver `docs/SDD.md`.
- `specs/` constitución + `spec.md`, `plan.md`, `tasks.md` por feature. Ver `docs/SDD.md`.

## Convenciones de código
- TypeScript estricto, prohibido `any` explícito o implícito.
- Server Components por defecto. Usa `"use client"` solo si hay
  interactividad, hooks o APIs de navegador.
- Archivos en `kebab-case`, componentes en `PascalCase`.
- Datos con `fetch` en servidor. Lógica compartida siempre en `lib/`.
- Estilos solo con Tailwind. Nada de CSS global extra salvo justificación.

## Patrones obligatorios
- Una ruta = una carpeta en `app/`. Lógica pesada fuera del componente.
- No duplicar lógica entre componentes, extrae a `lib/`.
- Funciones pequeñas, nombres explícitos, early returns.

## Prohibiciones
- No editar `package-lock.json` a mano.
- No poner secretos, tokens ni URLs privadas en código.
- No crear CSS custom si Tailwind lo resuelve.
- No crear archivos nuevos fuera de lo pedido sin preguntar.
- No inventar estructura Next.js real todavía.
- No añadir dependencias, frameworks o un paso de build in justificar alternativa con código propio y sin preguntar.

## Flujo de trabajo
1. Lee `MEMORY.md` para recuperar contexto y decisiones previas.
2. Cambio no trivial: aplica SDD paso a paso (`/sdd/spec` → clarify → `/sdd/plan` → `/sdd/tasks` → `/sdd/implement` → `/sdd/validate`), con aprobación en cada fase. Trivial: directo.
3. Haz cambios pequeños y verificables, un tema por vez.
4. Verifica con `npm run lint`, `npm run typecheck` y `npm test`.
5. Actualiza la sección de contexto en `MEMORY.md` al terminar.

## Testing y CI/CD
- `npm run lint`, `npm run typecheck` y `npm test` deben pasar en local.
- GitHub Actions bloquea el merge si falla lint, tipos o tests.
- No desactives reglas ni uses `skip-ci` sin aprobación explícita.

## Estilo de commits y PRs
- Commits: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`.
- Mensaje breve en imperativo, en inglés técnico.
- PRs con qué cambia, por qué, y cómo probarlo. Un tema por PR.
- Respuestas al usuario cortas, en español, código simple y legible.

## SDD (detalle en `specs/constitution.md`, `docs/SDD.md` y skill `sdd`)
- Feature real: loop paso a paso con comandos `/sdd/*` y aprobación explícita en cada fase. Nunca avances de fase sin aprobación.
- Trivial o prototipo: directo o spec-first (la spec muere tras generar).
- Si cambia el criterio, `/sdd/change` primero y regenera plan+tasks.
- Subagentes: coordinador (orquesta el flujo), planner (spec/plan/tasks), implementer (una tarea + TDD), reviewer (QA + validación RF); contexto entre fases vía `specs/NNN/`.
- En criterio de producto manda la constitución; en proceso manda este archivo.

## Memoria (detalle en skill `actualizar-memoria`)
- Al empezar, lee `MEMORY.md`. Al terminar, carga el skill `actualizar-memoria` y aplícalo.
- Mínimo seguro si el skill no carga: actualiza Estado, añade Decisiones con fecha y porqué, reescribe Contexto activo, no guardes secretos y resume lo viejo.

## Skills externas (mínimo del esqueleto)
- Las skills locales viven en `.opencode/skills/`. Para capacidades específicas usa skills.sh de forma modular y mantén limpio el contexto principal.
- Instala solo con el CLI `skills`: `npx skills add <owner>/<pack>` (ej. `npx skills add vercel-labs/agent-skills`). Lo instalado debe acabar siendo compatible con `.opencode/skills/`.
- Nunca instales una skill externa sin proponérmela antes y recibir aprobación. Revisa qué archivos trae y qué pide antes de instalar. Fija pack/versión si es crítico.

## MCP (detalle en `docs/MCP.md`, config en `.opencode/opencode.jsonc`)
- `context7` docs versionables · `devtools` navegador local (solo `localhost`) · `github` issues/PRs (lectura libre).
- Escritura y acciones con efecto solo con propuesta previa y aprobación. Secretos solo en env vars.
- El cómo usar cada MCP vive en su skill/comando, no aquí.
