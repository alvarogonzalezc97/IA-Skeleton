---
name: actualizar-memoria
description: Usar al terminar una tarea para actualizar MEMORY.md con estado, decisiones y contexto
---

# Actualizar memoria

Sigue estos pasos al terminar cada tarea para dejar `MEMORY.md` útil para la siguiente sesión.

## Qué actualizar

1. **Proyecto / Estado:** deja en una línea la versión y en qué punto queda (ej. `v0.4 — skills creadas, sin app real`).
2. **Decisiones tomadas:** añade una línea por decisión con fecha, qué se decidió y porqué en 1 línea. Ejemplo: `2026-10-05: skill X en español porque ...`.
3. **Contexto activo:** reescribe En curso y Siguiente paso. Borra lo ya hecho, no acumules historial aquí.
4. **Notas para el próximo agente:** máximo 4 avisos útiles (errores a evitar, qué no crear, qué validar).

## Qué podar

- Resume o elimina lo que ya no aporte. Si una nota lleva 3 versiones sin usarse, bórrala.
- No dupliques reglas de `AGENTS.md`. Si algo se vuelve regla permanente, propone moverlo a `AGENTS.md` en vez de dejarlo en memoria.

## Qué nunca guardar

- Claves, tokens, contraseñas, URLs privadas o datos personales. Si aparecen en el diff, omítelos y avisa.

## Ejemplo mínimo

```md
- **Estado:** v0.4 — 3 skills creadas, falta MCP.
## Decisiones tomadas
- 2026-10-05: memoria detallada en skill porque AGENTS debe quedar ligero.
## Contexto activo
- En curso: skills terminadas.
- Siguiente paso: MCP.
```
