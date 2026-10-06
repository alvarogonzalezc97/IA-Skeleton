---
name: tailwind-estilos
description: Usar al escribir o revisar estilos con Tailwind CSS, clases, responsive y estados
---

# Estilos Tailwind

Aplica estas reglas cuando escribas o revises clases y estilos.

## Base

- Solo Tailwind. Nada de CSS global extra ni `<style>` custom salvo justificación explícita.
- Clases legibles y ordenadas: layout primero, luego espaciado, tipografía, color, estados.
- Diseño `mobile-first`: base sin prefijo para móvil, luego `sm:`, `md:`, `lg:`.

## Estados y consistencia

- Incluye siempre estados interactivos en botones y enlaces: `hover:`, `focus-visible:`, `disabled:`.
- Reutiliza tokens (colores, espaciados) en vez de valores hardcodeados distintos en cada archivo.
- Si repites el mismo grupo de clases 3 veces, extrae un componente en `components/`.
- Si dudas de una clase o variante, verifícala con `context7` (Tailwind) antes de inventarla.

## Ejemplo bueno y malo

```tsx
// Mal: valores sueltos, sin estados, sin responsive
<button className="p-2 text-white" style={{ background: "#ff00aa" }}>Guardar</button>

// Bien: tokens, estados, responsive
<button className="rounded-lg bg-blue-600 px-4 py-2 text-white hover:bg-blue-700 focus-visible:outline-2 disabled:opacity-50 md:px-6">
  Guardar
</button>
```

## Errores a evitar

- Mezclar `style={{}}` con Tailwind para lo que Tailwind ya resuelve.
- Crear una clase CSS custom nueva en vez de componer utilidades.
- Olvidar `focus-visible` y `disabled` en elementos interactivos.
