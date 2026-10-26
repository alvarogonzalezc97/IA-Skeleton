# MEMORY.md — Memoria del proyecto para IA

> Este archivo es auto-contenido. Guarda el contexto entre sesiones.
> Si contradice a AGENTS.md, aplica AGENTS.md.

Memoria del proyecto entre sesiones. Resume o elimina lo que ya no aporte.

## Proyecto
- **Nombre:** IA-Skeleton (plantilla de desarrollo con IA)
- **Objetivo:** Esqueleto mínimo y documentado para trabajar con agentes IA.
- **Stack:** Next.js 16, React 19, TypeScript strict,
  Vite, Tailwind CSS, Node 24 LTS, npm, Prettier + ESLint, GitHub Actions.
- **Estado:** v0.8 — AGENTS.md + MEMORY.md + 11 comandos (familia `/sdd/*` + `/publicar-git`, `/nuevo-componente`) + 5 skills + MCP + SDD + subagentes, sin app real.
- **Estructura de referencia:** `app/` rutas, `components/` UI,
  `lib/` lógica, `public/` estáticos, `docs/` documentación del proyecto.
- **Idiomas:** documentación en español, código y commits en inglés técnico.

## Decisiones tomadas
- 2026-10-02: Empezar solo con AGENTS.md + MEMORY.md, sin app real.
- 2026-10-02: AGENTS.md y MEMORY.md son auto-contenidos, sin límite de líneas.
- 2026-10-02: La carpeta docs/ es solo para usuarios/desarrolladores, no para dar órdenes al agente.
- 2026-10-02: En conflicto, AGENTS.md tiene prioridad sobre MEMORY.md.
- 2026-10-05: Añadidos 4 comandos en español en `.opencode/commands/`: `feature`, `commit`, `nuevo-componente`, `revisa`.
- 2026-10-05: Creado `docs/COMANDOS.md` para humanos y renombrado `GUIA-ARCHIVOS-IA.md` a `GUIA-ESQUELETO.md`.
- 2026-10-05: Añadidas 3 skills en español: `nextjs-patterns`, `tailwind-estilos`, `actualizar-memoria`. Detalle de memoria movido al skill, en AGENTS queda gatillo + mínimo seguro anti-riesgo.
- 2026-10-05: Creado `docs/SKILLS.md` para humanos.
- 2026-10-05: Skills externas vía skills.sh como mínimo del esqueleto (CLI `npx skills add <owner>/<pack>`, con propuesta y aprobación previa).
- 2026-10-05: Eliminado comando `/revisa` a petición del usuario, limpiadas referencias en AGENTS y docs.
- 2026-10-05: Añadido MCP a nivel proyecto en `.opencode/opencode.jsonc`: `devtools` (local), `github` (remoto OAuth), `context7` (remoto). Creado `docs/MCP.md` detallado. Figma queda fuera por ahora.
- 2026-10-05: AGENTS adelgazado en MCP (solo enrutado + aprobaciones), detalle de `context7` movido a skills `nextjs-patterns` y `tailwind-estilos`.
- 2026-10-06: Añadido SDD: `specs/constitution.md`, ejemplo `specs/001-ejemplo-temas/`, comandos `/specify` y `/feature` (plan+tasks), skill `sdd`, `docs/SDD.md`. Constitución separada, AGENTS como enrutador.
- 2026-10-06: Constitución ampliada a 10 principios (simplicidad, spec manda, lógica pura, tests como puerta con `npm test`, idioma). Spec en formato EARS con numeración `NNN-nombre`. Prompt QA en `prompts/clarificar-spec.md`.
- 2026-10-06: Revisión QA del ejemplo (13 hallazgos) aplicada: spec EARS sin CÓMO, textos exactos de vacío/error, casos RF-3 a RF-7, CÓMO movido a `plan.md`, demo con checklist.
- 2026-10-06: Familia de 9 comandos `sdd-*` paso a paso (jubilados `/specify` y `/feature`, borrada `prompts/ssd/` absorbida). Skill `sdd` mezclada (puerta por fase, Estado, Definiciones, anti-palabras-vacías, Tn, >10→dividir, TDD por defecto con escape).
- 2026-10-06: Comandos SDD movidos a `.opencode/commands/sdd/` (se invocan `/sdd/*`), sin numerar (el orden vive en `SDD.md` y `/sdd/status`).
- 2026-10-06: Jubilado `/commit`, sustituido por `/publicar-git` (dos puertas + informa rama) y skill `publicar-git`.
- 2026-10-06: `/publicar-git` probado de punta a punta (commit `3057b0e` + push a `origin/main`): comandos shell con `;` en vez de `&&` (PowerShell), mensaje siempre en inglés.
- 2026-10-06: Prompts SDD en `prompts/ssd/` generalizados (rutas `specs/`, `npm test`, MCP `devtools`); AGENTS revisado (loop de vuelta a spec + precedencia acotada en cabecera).
- 2026-10-26: Cerrada documentación de subagentes (AGENTS, `docs/SDD.md`, README) y descartada seguridad/CI para el momento.
- 2026-10-26: Corregido YAML inválido en los 4 ficheros de `.opencode/agents/` (indentación de `permissions` rota el parseo → "cannot run as a subagent"). Tras arreglarlo, el ciclo con subagentes funciona.
- 2026-10-26: Ciclo SDD con subagentes sobre el ejemplo `001-ejemplo-temas`: 3 rondas de QA (reviewer) + correcciones (planner). RF-7 retirado por duplicar RF-1; spec queda VEREDICTO: APROBADO; sugerencias opcionales aplicadas (RF-2 "temas válidos", checklist cita RF-1+RF-4) y Estado actualizado. plan.md/tasks.md coherentes.
- 2026-10-26: Decisión: la spec de ejemplo NO se implementa todavía (esqueleto sin app real). El implementer paró correctamente en T1 al no existir proyecto npm (`node --test`/typecheck imposibles). Implementación queda para cuando se decida el bootstrap.

## Contexto activo
- En curso: SDD terminada.
- Siguiente paso: primera página o ejemplo real con Next.js.
- Aviso: no crear estructura Next.js real todavía, solo usarla como referencia.

## Notas para el próximo agente
- Mantener respuestas cortas y código simple y legible.
- Hacer cambios pequeños, un tema por vez.
- Pedir aclaración antes de crear archivos nuevos fuera de lo pedido.
- Al terminar cada tarea, actualizar Contexto activo y Decisiones si hay nuevas.
