# Tareas: listado de temas (ejemplo)

Ordenadas y verificables. Una por vez.

- [ ] 1. Crear `lib/temas.ts` con tipo `Tema` y `getTemas()` pura de ejemplo.
  Verificar: `npm run typecheck` y `npm test` pasan.
- [ ] 2. Crear `components/theme-card.tsx` Server con Tailwind.
  Verificar: renderiza título y descripción; sin título no se usa (RF-4 en página).
- [ ] 3. Crear `app/temas/page.tsx` con listado + estado vacío (RF-1, RF-2).
  Verificar: con 0 y 3 temas se comporta según spec.
- [ ] 4. Añadir estado de error (RF-3) y casos RF-5/RF-6.
  Verificar: cada RF con su test en verde.
- [ ] 5. Pasar `lint`, `typecheck`, `tests` y validar contra `spec.md`
  con el checklist de criterios de finalización.
