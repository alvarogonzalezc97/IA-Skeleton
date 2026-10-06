---
description: Crea un componente Next.js siguiendo las convenciones
---

Crea el componente llamado: $ARGUMENTS.

Reglas (según AGENTS.md):
1. Server Component por defecto. Usa `"use client"` solo si hay interactividad, hooks o APIs de navegador.
2. Ubicación: `components/<nombre-en-kebab-case>.tsx`, nombre del componente en `PascalCase`.
3. Estilos solo con Tailwind. Lógica compartida en `lib/`, no dentro del componente.
4. TypeScript estricto, sin `any`. Funciones pequeñas y nombres explícitos.
5. Si el nombre viene vacío o no sigue la convención, pídeme aclaración antes de crearlo.
