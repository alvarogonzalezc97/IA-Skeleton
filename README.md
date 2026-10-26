# IA-Skeleton

Esqueleto mínimo para trabajar con agentes de IA en desarrollo de software.

## Qué es

Punto de partida con las piezas mínimas que ya usa un equipo moderno para
desarrollar con IA: reglas para el agente, memoria persistente, comandos,
skills, MCP y flujo spec-driven (SDD).

## Estado

Versión actual: **v0.7** — reglas + memoria + comandos + skills + MCP + SDD + subagentes.

## Contenido

- `AGENTS.md`: reglas del agente (stack, estructura, convenciones, flujo).
- `MEMORY.md`: memoria persistente entre sesiones.
- `specs/`: constitución del proyecto + specs por feature (`NNN-nombre/`).
- `.opencode/commands/`: comandos tipo `/sdd/*` y `/publicar-git`.
- `.opencode/skills/`: skills (`sdd`, `publicar-git`, `nextjs-patterns`, …).
- `.opencode/agents/`: subagentes SDD (`coordinador`, `planner`, `implementer`, `reviewer`).
- `.opencode/opencode.jsonc`: config MCP a nivel proyecto.
- `docs/`: documentación humana (comandos, skills, MCP, SDD, etc.).
- `prompts/`: prompts de ejemplo.

## Uso rápido

- Cambio no trivial: loop SDD paso a paso (`/sdd/spec` → clarify → `/sdd/plan` → `/sdd/tasks` → `/sdd/implement` → `/sdd/validate`) con aprobación en cada fase.
- Trivial: cambio directo, sin SDD.
- Publicar (A modo de ejemplo): `/publicar-git` (dos puertas: propuesta de commit → aprobación → push).
