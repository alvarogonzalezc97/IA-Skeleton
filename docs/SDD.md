# SDD (Spec-Driven Development)

Guía para personas. Taxonomía, pasos y cómo se usan en este esqueleto.
Hogar de artefactos: `specs/`. Constitución: `specs/constitution.md`.

## Taxonomía: spec-first vs SDD

- **Spec-first:** escribes la especificación, generas el código una vez
  y a partir de ahí editas el código directamente. La spec fue el punto
  de partida y muere. Rápido, desechable.
- **SDD:** la spec vive y manda. Cambia el criterio → cambia la spec
  primero, luego plan, tareas y código. Para features reales.

Cuándo usar cada uno:

| Caso | Modo |
| ---- | ---- |
| Prototipo, prueba, cambio trivial | Directo o spec-first |
| Feature real, criterio que debe durar | SDD completo |

## Pasos SDD

1. **Constitución** (`specs/constitution.md`, una vez por proyecto):
   principios inmutables de producto y calidad.
2. **Especificación** (`specs/NNN-<feature>/spec.md`): contexto,
   usuarios e historias, requisitos en EARS (CUANDO/SI/MIENTRAS/EL SISTEMA),
   casos límite, fuera de alcance y criterios de finalización. Sin tecnología ni código.
3. **Clarificación** (con compuerta): solo si hay ambigüedades
   bloqueantes, se preguntan antes de planificar. Si está clara, se salta.
4. **Planificación** (`specs/NNN-<feature>/plan.md`): CÓMO, derivado de
   spec + constitución + skills/MCP. Archivos y riesgos.
5. **Tareas** (`specs/NNN-<feature>/tasks.md`): pasos pequeños, ordenados
   y verificables, cada uno con su comprobación.
6. **Implementación**: tarea a tarea, con skills y MCP que encajen.
7. **Validación**: criterios de la spec + `lint`, `typecheck`, `tests`.

## Loop (mantenimiento)

El mantenimiento no es un paso, es lo que provoca volver al Paso 2:
ante cualquier cambio de criterio, bug de criterio o deriva,
re-entra por spec → clarify → plan → tasks → implement → validate.
Nunca cambies código sin actualizar la spec cuando cambia el criterio.

```text
constitution (1 vez)
  → spec → clarify? → plan → tasks → implement → validate
  → ante cambio: volver a spec (loop)
```

## Comandos y skills

- `/sdd/constitution` → propone o revisa `specs/constitution.md`.
- `/sdd/spec NNN-nombre idea` → entrevista y crea `spec.md` en `borrador`.
- `/sdd/clarify NNN-nombre` → revisión QA, solo detecta.
- `/sdd/plan NNN-nombre` → crea `plan.md` (solo con spec aprobada).
- `/sdd/tasks NNN-nombre` → crea `tasks.md` (Tn + "Hecho cuando", máx 10).
- `/sdd/implement NNN-nombre Tn` → implementa UNA tarea y para.
- `/sdd/validate NNN-nombre` → veredicto RF por RF.
- `/sdd/change NNN-nombre requisito` → actualiza la spec primero, muestra diff.
- `/sdd/status NNN-nombre` → fase actual y siguiente paso, sin modificar nada.
- Skill `sdd` → la IA la carga sola al trabajar en `specs/`.
- Ejemplo completo: `specs/001-ejemplo-temas/` (spec, plan, tasks).

## Subagentes

El flujo SDD se ejecuta con cuatro subagentes (definidos en `.opencode/agents/`):

- **Coordinador:** orquesta el loop completo (spec → clarify → plan → tasks → implement → validate) delegando en planner, implementer y reviewer. Gestiona las puertas de aprobación con el usuario.
- **Planner:** redacta spec/plan/tasks desde una petición. No toca código.
- **Implementer:** implementa UNA tarea de un plan aprobado, con TDD, y para.
- **Reviewer:** revisa la spec como QA y valida la implementación RF por RF, sin modificar nada.

## Cómo probarlo

1. `/sdd/spec 002-listado-temas listado de temas` → revisa `spec.md` en `borrador`.
2. `/sdd/clarify 002-listado-temas` → lista numerada de hallazgos.
3. Aprueba, `/sdd/plan` → `/sdd/tasks` → `/sdd/implement 002-listado-temas T1` → `/sdd/validate`.
4. Cambia un criterio con `/sdd/change` y comprueba que plan/tareas se revisan.
