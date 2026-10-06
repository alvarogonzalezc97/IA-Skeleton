# Plan: listado de temas (ejemplo)

Derivado de `spec.md` + `specs/constitution.md` + skills.

## Enfoque

Server Component en `app/temas/page.tsx` (sin `"use client"`) que llama a
una función pura `getTemas()` en `lib/temas.ts` y renderiza `ThemeCard`
por tema. Datos de ejemplo locales, sin API externa.

## Archivos

- `lib/temas.ts` → tipo `Tema` + `getTemas()` pura (sin DOM ni storage).
- `components/theme-card.tsx` → tarjeta Server, Tailwind.
- `app/temas/page.tsx` → página Server con listado, estado vacío y estado de error.

## Riesgos

- Ninguno relevante. El CÓMO (Server, `fetch`/origen local, `lib/`, sin `any`)
  vive aquí por principio 4 de la constitución, no en la spec.
