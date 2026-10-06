---
name: publicar-git
description: Usar al publicar cambios en git - mensajes, puertas de aprobación, ramas y push
---

# Publicar en git

Aplica este criterio al publicar cambios con `/publicar-git`.

## Mensaje de commit

- Un solo tipo: `feat:`, `fix:`, `docs:`, `refactor:`, `test:` o `chore:`.
- Breve, en imperativo, en inglés técnico.
- Si hay varios temas mezclados, propone separarlos en vez de un solo commit.

## Puertas (obligatorias)

1. **Puerta 1 (commit):** muestra rama actual (`git branch --show-current`),
   archivos del `status`/`diff` y mensaje propuesto. No commitees sin aprobación.
2. **Puerta 2 (push):** muestra rama destino exacta. No pushees sin aprobación.

## Ramas y push

- Publica siempre en la rama actual e infórmala en cada puerta. Nunca asumas `main`.
- Primera vez: `git push -u origin <rama>`. Después: `git push` a secas.
- Prohibido `--force` sin aprobación explícita y justificada.

## Seguridad

- Revisa `.gitignore` antes del `add`. Si falta (ej. `.env`), avisa y para.
- Nunca publiques secretos, tokens ni URLs privadas. Si aparecen en el diff, omite esos archivos y avisa.

## Errores a evitar

- `git add -A` sin haber mostrado antes qué entra.
- Commit y push del tirón sin puertas.
- Pushear a una rama distinta de la anunciada.
