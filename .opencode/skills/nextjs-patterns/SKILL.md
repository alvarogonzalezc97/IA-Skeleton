---
name: nextjs-patterns
description: Usar al crear páginas, layouts, componentes o fetch de datos en Next.js 16 con App Router y React 19
---

# Patrones Next.js

Aplica estas reglas cuando crees o modifiques código en `app/`, `components/` o `lib/`.

## Server por defecto

- Server Component salvo que necesites interactividad, hooks (`useState`, `useEffect`) o APIs de navegador. Solo entonces usa `"use client"` en la primera línea.
- Los datos se obtienen en el servidor con `fetch` o funciones en `lib/`. Nunca hagas fetch en el cliente si puedes hacerlo en el servidor.

## Organización

- Una ruta = una carpeta en `app/`. Ejemplo: `app/temas/[slug]/page.tsx`.
- Componentes reutilizables en `components/<nombre-kebab-case>.tsx`, componente en `PascalCase`.
- Lógica de negocio, helpers y acceso a datos en `lib/`. No dejes lógica pesada dentro del componente.
- Funciones pequeñas, nombres explícitos, early returns. No duplicar lógica entre componentes.

## TypeScript

- Modo estricto, prohibido `any` explícito o implícito. Define tipos de props y de retorno de `fetch`.
- Si un tipo se complica, divídelo en tipos pequeños en `lib/`.
- Ante duda versionable de API, prop o config de Next/React, consulta `context7` antes de responder.

## Ejemplo bueno

```tsx
// components/theme-card.tsx (Server Component)
import { getTheme } from "@/lib/temas";

export async function ThemeCard({ slug }: { slug: string }) {
  const tema = await getTheme(slug);
  if (!tema) return null;
  return <article className="rounded-lg border p-4">{tema.titulo}</article>;
}
```

## Errores a evitar

- Marcar todo como `"use client"` por comodidad.
- Hacer fetch en el cliente o duplicar la misma llamada en varios componentes.
- Poner acceso a datos dentro de `components/` en vez de `lib/`.
