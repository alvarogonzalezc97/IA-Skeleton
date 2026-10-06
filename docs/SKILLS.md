# Skills

Guía para personas. Explica qué skills existen, cuándo las usa la IA y cómo crear una nueva. Diferencia con comandos en `COMANDOS.md`.

## Qué son

Piezas de conocimiento que la IA carga sola cuando encajan con la tarea.
Cada skill es una carpeta en `.opencode/skills/<id>/SKILL.md` con una
`description` que sirve para descubrirla. No las invocas tú con `/`,
la IA las carga con el tool `skill`. Tú puedes forzarlas con `@id`.

Diferencia rápida:

```text
Comando /sdd/spec  -> lo pides tú, ejecuta una acción concreta
Skill @nextjs-patterns -> la IA la carga sola al crear una página
```

## Skills disponibles

### `sdd`

Cuándo se carga: al trabajar con especificaciones, planes o tareas en `specs/`.
Aporta: el loop SDD (spec → clarify → plan → tasks → implement → validate)
y errores a evitar.

Pruébalo forzando: `@sdd revisa esta spec`.

### `publicar-git`

Cuándo se carga: al publicar cambios con `/publicar-git`.
Aporta: formato de mensaje, dos puertas obligatorias, ramas (informa
siempre la destino, nada de `--force`), `.gitignore` y secretos.

Pruébalo forzando: `@publicar-git revisa qué se publicaría ahora`.

### `nextjs-patterns`

Cuándo se carga: al crear páginas, layouts, componentes o fetch de datos.
Aporta: Server por defecto, `fetch` en servidor, organización `app/` /
`components/` / `lib/`, TypeScript estricto, nombres y errores a evitar.

Pruébalo forzando: `@nextjs-patterns crea la página de temas`.

### `tailwind-estilos`

Cuándo se carga: al escribir o revisar estilos.
Aporta: solo Tailwind, orden de clases, `mobile-first`, estados
`hover/focus/disabled`, tokens en vez de hardcodeados, ejemplo bueno/malo.

Pruébalo forzando: `@tailwind-estilos revisa este botón`.

### `actualizar-memoria`

Cuándo se carga: al terminar una tarea y actualizar `MEMORY.md`.
Aporta: qué escribir en Estado / Decisiones / Contexto activo, qué podar,
qué no guardar nunca y cuándo proponer mover una regla a `AGENTS.md`.

Pruébalo forzando: `@actualizar-memoria actualiza la memoria con lo hecho hoy`.

## Cómo probar que funcionan

1. Abre el proyecto en OpenCode.
2. Pide algo que encaje (`crea un componente ThemeCard`, `actualiza la memoria`).
3. Comprueba que la IA menciona o aplica el skill correspondiente.
4. Si no lo carga, fórzalo con `@id` y revisa que el archivo exista en
   `.opencode/skills/<id>/SKILL.md` con `description`.

## Cómo crear una skill nueva

1. Crea `.opencode/skills/mi-skill/SKILL.md`.
2. Empieza con nombre y descripción clara (la descripción es lo que la hace discoverable):

```md
---
name: Mi skill
description: Usar cuando ... (cuándo debe cargarse)
---

# Título

Reglas cortas, ejemplo bueno/malo, errores a evitar.
```

3. Usa IDs en minúsculas con guiones, igual que la carpeta (`mi-skill`).
4. Mantenla corta y con ejemplos. Si necesita archivos de apoyo, ponlos al
   lado en `references/` o `scripts/` (rutas relativas al `SKILL.md`).

## Relación con el resto del esqueleto

- `AGENTS.md` dice *cuándo* cargar cada skill (gatillo mínimo anti-riesgo).
- El skill dice *cómo* hacerlo en detalle.
- `MEMORY.md` es lo que `actualizar-memoria` mantiene al día.
- Los comandos (`COMANDOS.md`) piden acciones, los skills aportan criterio.

## Skills externas y modulares (skills.sh)

Con plataformas como skills.sh dotas al agente de habilidades específicas
de forma modular, sin inflar el contexto principal. Solo se cargan cuando tocan.

Para instalar skills en nuestro agente usamos el CLI `skills`:

```sh
npx skills add vercel-labs/agent-skills
```

- `skills` es el CLI, `vercel-labs/agent-skills` es un pack de ejemplo.
- Busca packs en https://www.skills.sh/docs e instala solo lo que necesites.
- Revisa qué archivos trae cada skill antes de instalarla.
- Lo instalado debe acabar siendo compatible con `.opencode/skills/`.
