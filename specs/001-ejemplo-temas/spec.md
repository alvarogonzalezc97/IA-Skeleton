# Spec 001 — Listado de temas (ejemplo)

Estado: aprobada (ejemplo corregido tras revisión QA).

Feature de ejemplo para mostrar el hogar SDD. No implementada.

## Contexto y objetivo

Necesitamos una página que muestre los temas disponibles con su título
y descripción, para validar el flujo SDD de punta a punta con un caso simple.

## Usuarios / actores

- Visitante que navega el listado de temas.

## Historias de usuario

- H1: Como visitante quiero ver el listado de temas para elegir cuál leer.

## Requisitos funcionales (criterios de aceptación en EARS)

- RF-1: CUANDO el visitante abre la página de temas, EL SISTEMA muestra una tarjeta por cada tema válido con su título y descripción, en el orden que devuelve el origen de datos.
- RF-2: SI no hay temas, ENTONCES EL SISTEMA muestra el texto exacto "No hay temas todavía.".
- RF-3: SI la carga de temas falla, ENTONCES EL SISTEMA muestra el texto exacto "No se pudieron cargar los temas.".
- RF-4: SI un tema no tiene título, ENTONCES EL SISTEMA omite esa tarjeta y muestra el resto.
- RF-5: SI un tema no tiene descripción, ENTONCES EL SISTEMA muestra su tarjeta solo con el título.
- RF-6: MIENTRAS haya temas duplicados en el origen, EL SISTEMA los muestra tal cual, sin deduplicar.
- RF-7: EL SISTEMA muestra el número de tarjetas igual al número de temas válidos del origen.

## Requisitos no funcionales

- Origen de datos: datos de ejemplo locales en `lib/` (sin API externa ni paquetes nuevos).
- Obtención testeable con `npm test` sin navegador.
- Idioma: interfaz en español, código en inglés.

## Casos límite

- 0 temas → RF-2.
- Fallo de carga → RF-3.
- Tema sin título → RF-4. Tema sin descripción → RF-5.
- Duplicados → RF-6. Listado grande → se renderiza completo (sin paginación en esta iteración).

## Fuera de alcance

- Sin paginación, sin buscador, sin detalle de tema.
- Sin autenticación ni escritura de datos.

## Criterios de finalización

- Todos los RF con `npm test` en verde + `lint` y `typecheck` en verde.
- Demo manual con checklist: (1) abrir `/temas` con 3 temas → 3 tarjetas con título y descripción; (2) con origen vacío → "No hay temas todavía."; (3) con un tema sin título → se omite solo esa tarjeta.

## Dudas abiertas

- Ninguna. Ambigüedades de la revisión QA (origen, orden, textos, error de carga) resueltas arriba.
