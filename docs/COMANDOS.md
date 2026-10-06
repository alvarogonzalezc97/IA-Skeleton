# Comandos personalizados

Guía para personas. Explica qué comandos existen, cómo usarlos y cómo crear uno nuevo.

## Qué son

Atajos que se invocan en OpenCode con `/nombre`. Cada comando es un archivo
markdown en `.opencode/commands/` (o subcarpetas: `sdd/spec.md` se usa
como `/sdd/spec`). El contenido del archivo es la
instrucción que recibe la IA, con `$ARGUMENTS` para lo que escribas detrás.

Ejemplo: escribes `/sdd/spec 002-login login con email`, OpenCode envía a la IA la
plantilla de `sdd/spec.md` con `002-login` en `$1` y `login con email` en `$2`.

## Comandos disponibles

### Familia SDD (`/sdd/*`, detalle en `SDD.md`)

| Comando | Fase |
| ------- | ---- |
| `/sdd/constitution` | Propone la constitución (principios innegociables) |
| `/sdd/spec 002-nombre idea` | Entrevista y genera `spec.md` en `borrador` |
| `/sdd/clarify 002-nombre` | Revisión QA (solo detecta, no resuelve) |
| `/sdd/plan 002-nombre` | Genera `plan.md` desde spec aprobada |
| `/sdd/tasks 002-nombre` | Divide en tareas `Tn` verificables (máx 10) |
| `/sdd/implement 002-nombre T3` | Implementa UNA tarea y para |
| `/sdd/validate 002-nombre` | Veredicto RF por RF |
| `/sdd/change 002-nombre requisito` | Nuevo requisito: primero la spec |
| `/sdd/status 002-nombre` | Fase actual y siguiente paso (solo lee) |

### `/publicar-git`

Publica los cambios con dos puertas usando la skill `publicar-git`:
revisa `.gitignore`+`status`/`diff`, propone archivos y mensaje (puerta 1),
commitea tras aprobar, y pushea a la rama actual tras segunda aprobación.
Siempre informa en qué rama se sube. Nunca `--force` sin permiso.

Ejemplo:

```text
/publicar-git
```

### `/nuevo-componente <Nombre>`

Crea un componente Next.js siguiendo `AGENTS.md`: Server Component por
defecto, `kebab-case` para el archivo, `PascalCase` para el componente,
Tailwind y TypeScript estricto.

Ejemplo:

```text
/nuevo-componente ThemeCard
```

## Cómo probar que funcionan

1. Abre el proyecto en OpenCode.
2. Escribe `/sdd/spec 002-prueba idea de prueba` y comprueba que crea `specs/002-prueba/spec.md` en `borrador` sin código.
3. Escribe `/sdd/status 002-prueba` y comprueba que indica fase y siguiente paso.
4. Haz un cambio pequeño y prueba `/publicar-git` hasta la puerta 1 (sin aprobar).
5. Si un comando no aparece, comprueba que el archivo esté en
   `.opencode/commands/` y termine en `.md`.

## Cómo crear un comando nuevo

1. Crea `.opencode/commands/mi-comando.md`.
2. Empieza con una descripción:

```md
---
description: Qué hace mi comando
---

Haz algo con: $ARGUMENTS.
```

3. Usa `$ARGUMENTS` para el texto completo o `$1`, `$2` para posiciones.
4. Puedes insertar salida de shell con `` !`comando` `` (ej. `git diff`).
5. Guarda y úsalo como `/mi-comando ...` sin reiniciar.

## Relación con el resto del esqueleto

- `AGENTS.md` define las reglas que los comandos deben respetar.
- `MEMORY.md` guarda el estado que la familia `/sdd/*` lee y actualiza.
- Esta carpeta `docs/` es solo para humanos, los comandos viven en `.opencode/`.
