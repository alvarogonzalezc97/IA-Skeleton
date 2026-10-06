---
description: SDD · Valida la spec RF por RF (tests + devtools)
---

Recorre `specs/$1/spec.md` requisito por requisito. Para cada RF indica qué test
lo cubre y el resultado de ejecutarlo con `npm test`.
Los RF de interfaz que no se puedan testear con `npm test`, verifícalos con
el MCP `devtools` (solo localhost, incluida la vista móvil de 375 px).
Si algún RF no está cubierto o falla, dilo claramente. NO arregles nada todavía.
Después comprueba los criterios de finalización y dame un veredicto:
¿la spec está cumplida? Si todo está en verde, propón marcarla como implementada.
