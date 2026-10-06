# Guía del esqueleto

Guía para personas que llegan nuevas al proyecto IA-Skeleton.
Explica cada pieza y cómo encajan. Detalle de comandos en `COMANDOS.md`, de skills en `SKILLS.md`, de MCP en `MCP.md` y de SDD en `SDD.md`.

## Qué es este esqueleto

Un punto de partida mínimo para desarrollar software con ayuda de la IA,
sin que cada sesión parta de cero ni cada agente invente sus reglas.
Versión actual v0.7: reglas + memoria + comandos + skills + MCP + SDD, aún sin aplicación real.

## Qué hay en el proyecto

- `AGENTS.md`: Manual que sigue la IA. Define stack, estructura,
  convenciones, prohibiciones, flujo de trabajo, testing y commits.
  Es auto-contenido y tiene prioridad si hay contradicciones.
- `MEMORY.md`: Cuaderno del proyecto. Guarda objetivo, decisiones
  con fecha, estado actual y siguiente paso. Sirve para retomar
  el trabajo entre sesiones.
- `.opencode/commands/`: Familia `/sdd/*` (9 comandos en `sdd/`, ver `COMANDOS.md`),
  más `/publicar-git` y `/nuevo-componente`.
- `.opencode/skills/`: Skills `sdd`, `publicar-git`, `nextjs-patterns`,
  `tailwind-estilos`, `actualizar-memoria`. Ver `SKILLS.md`.
- `.opencode/opencode.jsonc`: Config MCP a nivel proyecto
  (`devtools`, `github`, `context7`). Ver `MCP.md`.
- `specs/`: Constitución + `spec.md`, `plan.md`, `tasks.md` por feature.
  Ver `SDD.md`.
- `docs/`: Documentación para personas.

## Cómo interactúan (visto desde fuera)

```text
El agente lee AGENTS.md  -> sabe cómo debe trabajar
El agente lee MEMORY.md  -> sabe en qué punto quedó el proyecto
Hace la tarea y actualiza MEMORY.md -> el siguiente puede continuar
```

Totalmente automatizado, de manera que no es necesario repetirle las reglas, ya están escritas.

## Cómo empezar como nuevo desarrollador

1. Lee `AGENTS.md` para conocer stack y convenciones.
2. Lee `MEMORY.md` para saber estado y decisiones tomadas.
3. Lee `COMANDOS.md` para ver la familia `/sdd/*`, `/publicar-git`, etc.
4. Lee `SKILLS.md` para ver qué criterio aporta cada skill.
5. Lee `MCP.md` para ver qué herramientas externas hay y cómo probarlas.
6. Lee `SDD.md` para ver cómo trabajar con specs.
7. Propón el siguiente paso (ej. primera página real).

## Ejemplo orientativo con Next.js

La estructura de referencia es `app/`, `components/`, `lib/`, `public/`.
Por ejemplo, una futura página `app/temas/[slug]/page.tsx` sería un
Server Component con estilos Tailwind y lógica en `lib/`.
No existe aún, es solo para imaginar cómo se organizará el código.

## Cómo evoluciona el esqueleto

Se mejora poco a poco: primero reglas y memoria, después comandos,
después skills, MCP y SDD, ahora ejemplos reales. Cada cambio de criterio
debe quedar registrado con fecha en `MEMORY.md`.
