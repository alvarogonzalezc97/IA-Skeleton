# Constitución del proyecto (SDD Paso 1)

Principios inmutables. Se define una vez y solo cambia con decisión
explícita registrada en `MEMORY.md`. El detalle operativo vive en
`AGENTS.md` y en las skills; aquí van los criterios de producto.

## Principios

1. Simplicidad primero. Menos es más: recortar es una decisión válida
   en cada paso. Nada de anticipar casos que la spec no pide.
2. La spec manda: nada se implementa si no está en la spec activa.
   Si falta una decisión, se para y se pregunta. Nunca se inventa.
3. Spec-first para lo desechable, SDD con spec viva para lo real.
   Trivial o prototipo → directo o spec de un uso que muere.
   Feature real → spec viva: cambia el criterio, cambia la spec primero.
4. La spec describe QUÉ y PORQUÉ, nunca CÓMO. Sin nombres de funciones,
   sin decisiones de librería, sin código.
5. Lógica separada de interfaz: los cálculos son funciones puras en
   `lib/`, sin DOM ni storage, con dependencias inyectadas
   (ej. la fecha actual como parámetro, no leída dentro).
6. Tests como puerta: `npm run lint`, `npm run typecheck` y `npm test`
   en verde antes de dar nada por válido. Prohibido avanzar con tests
   en rojo. Sin instalar paquetes de test.
7. Todo criterio debe ser verificable. Si no se puede comprobar,
   no es un criterio, es un deseo: se reescribe o se elimina.
8. Alcance explícito: toda spec declara su fuera de alcance. Lo que no
   está en la spec no se implementa sin aprobar ampliación de spec.
9. Tareas pequeñas y ordenadas. Ninguna tarea supera media sesión de
   trabajo ni mezcla dos temas.
10. Idioma: código en inglés; interfaz y documentación en español.

## Stack y calidad (resumen, detalle en `AGENTS.md`)

- Next.js 16 + React 19 + TypeScript estricto + Tailwind.
- Server Components por defecto, lógica en `lib/`, sin `any`.
- Las specs de feature viven en `specs/NNN-nombre/` (`spec.md`,
  `plan.md`, `tasks.md` numeradas por orden de creación).

## Precedencia

- En criterio de producto manda esta constitución.
- En proceso de trabajo manda `AGENTS.md`.
- En memoria entre sesiones manda `MEMORY.md` actualizado vía skill.
