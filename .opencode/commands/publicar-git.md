---
description: Publica los cambios con dos puertas - propone commit, espera aprobación, pushea a la rama actual
---

Publica los cambios actuales. Usa la skill `publicar-git`. $ARGUMENTS

Sigue estas reglas:
1. Paso 0: revisa `.gitignore`, `git status` y `git diff --stat`:

!`git status --short; git diff --stat; git branch --show-current`

2. Puerta 1: dime rama actual, archivos que entrarían y el mensaje propuesto.
   NO hagas commit todavía: espera mi aprobación.
3. Tras aprobar: `git add -A` (solo lo revisado) y commit con ese mensaje.
4. Puerta 2: dime rama destino exacta y pide aprobación para el push.
   Tras aprobar: `git push` (con `-u origin <rama>` la primera vez).
   Nunca `--force` sin aprobación explícita.
