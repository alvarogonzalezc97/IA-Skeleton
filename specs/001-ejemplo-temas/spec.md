# Spec 001 — Listado de temas (ejemplo)

Estado: aprobada (re-revisión con subagentes: 3 rondas de QA; RF-7 retirado por duplicar RF-1; 2 sugerencias opcionales aplicadas).

Feature de ejemplo para mostrar el hogar SDD. No implementada.

## Contexto y objetivo

Necesitamos una página que muestre los temas disponibles con su título
y descripción, para validar el flujo SDD de punta a punta con un caso simple.

## Usuarios / actores

- Visitante que navega el listado de temas.

## Historias de usuario

- H1: Como visitante quiero ver el listado de temas para elegir cuál leer.

## Definiciones (solo si hay términos que puedan interpretarse de varias formas)

- Tema válido: tema con título presente (no nulo ni vacío); un tema sin título se omite del listado (ver RF-4).
- Título: dato textual que identifica al tema; sin él, el tema no es válido.
- Descripción: dato opcional asociado al tema; su ausencia no invalida el tema.

## Requisitos funcionales (criterios de aceptación en EARS)

- RF-1: CUANDO el visitante abre la página de temas, EL SISTEMA muestra una tarjeta por cada tema válido con su título y descripción, en el orden en que se declaran los temas en los datos de ejemplo locales.
- RF-2: SI no hay temas válidos (o no hay temas), ENTONCES EL SISTEMA muestra el texto exacto "No hay temas todavía.".
- RF-3: SI la carga de temas falla, ENTONCES EL SISTEMA muestra el texto exacto "No se pudieron cargar los temas.".
- RF-4: SI un tema no tiene título (nulo o vacío), ENTONCES EL SISTEMA omite esa tarjeta y muestra el resto.
- RF-5: SI un tema no tiene descripción (nulo o vacío), ENTONCES EL SISTEMA muestra su tarjeta solo con el título.
- RF-6: MIENTRAS haya temas duplicados en el origen, EL SISTEMA los muestra tal cual, sin deduplicar.

## Requisitos no funcionales

- Origen de datos: datos de ejemplo locales, sin API externa.
- Obtención testeable con `npm test` sin navegador.
- Idioma: interfaz en español, código en inglés.

## Casos límite

- 0 temas → RF-2.
- Fallo de carga → RF-3.
- Tema sin título → RF-4. Tema sin descripción → RF-5.
- Todos los temas se omiten por falta de título → se aplica RF-2 (se muestra "No hay temas todavía.").
- Duplicados → RF-6. Listado grande → se renderiza completo (sin paginación en esta iteración).

## Fuera de alcance

- Sin paginación, sin buscador, sin detalle de tema.
- Sin autenticación ni escritura de datos.

## Criterios de finalización

- Todos los RF con `npm test` en verde + `lint` y `typecheck` en verde.
- Demo manual con checklist: (1) abrir `/temas` con 3 temas → 3 tarjetas con título y descripción; (2) con origen vacío → "No hay temas todavía."; (3) con un tema sin título → se omite solo esa tarjeta; (4) con un tema sin descripción → se muestra solo con el título; (5) con temas duplicados → se muestran todos; (6) con fallo de carga → "No se pudieron cargar los temas."; (7) deriva de RF-1+RF-4: con 3 temas de origen y uno sin título → se muestran 2 tarjetas, coincidiendo con el número de temas válidos.

## Dudas abiertas

- Ninguna. Ambigüedades de la revisión QA (origen, orden, textos, error de carga) resueltas arriba.
