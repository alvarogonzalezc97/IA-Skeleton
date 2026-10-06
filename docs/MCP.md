# MCP (Model Context Protocol)

Guía para personas. Explica qué servidores MCP usa el proyecto, para qué
sirve cada uno, cómo probarlos y cómo añadir uno nuevo. La config vive en
`.opencode/opencode.jsonc` (nivel proyecto).

## Qué es MCP en 5 líneas

1. MCP conecta al agente con herramientas externas (navegador, GitHub, docs).
2. Cada servidor expone herramientas con nombre `servidor_herramienta`.
3. Las herramientas consumen contexto, así que solo activamos las necesarias.
4. Los servidores remotos usan OAuth por defecto, las claves van en env vars.
5. Con `/mcps` ves estado, conectas y autenticas cada servidor.

## Servidores activos

| Servidor   | Para qué                         | Cuándo lo usa la IA                  | Efecto   |
| ---------- | -------------------------------- | ------------------------------------ | -------- |
| `devtools` | Navegador real (Chrome DevTools) | Probar páginas, consola, accesibilidad | Lectura + navegación local |
| `github`   | Issues, PRs, ramas, checks       | Gestionar issues y PRs del repo      | Lectura + escritura con aprobación |
| `context7` | Docs actualizadas de librerías   | Resolver dudas de Next/React/Tailwind | Solo lectura |

### `devtools` — ejemplo clásico de MCP

Automatiza un navegador Chromium: abre URLs, hace click, lee consola,
mide rendimiento y revisa accesibilidad.

Qué puede hacer:

```text
Abre http://localhost:3000/temas y dime errores de consola
Haz click en el botón Guardar y dime qué pasa en red
Revisa accesibilidad de la página de temas
```

Qué NO debe hacer:

- Navegar fuera de `localhost` sin tu aprobación explícita.
- Rellenar formularios reales ni aceptar diálogos sin permiso.

Cómo probarlo:

1. Levanta la app (`npm run dev` cuando exista).
2. En OpenCode ejecuta `/mcps` y comprueba `devtools connected`.
3. Pide `abre http://localhost:3000 y dime el título y errores de consola`.

Si falla la conexión, es un servidor local (`npx chrome-devtools-mcp`).
Requiere Node 20+ y que el puerto esté libre.

### `github` — issues, PRs y ramas

Gestiona el repo sin salir del agente: lista issues, crea ramas,
abre PRs y revisa checks.

Qué puede hacer:

```text
Lista las issues abiertas del repo
Crea una PR de esta rama con qué cambia, por qué y cómo probarlo
Revisa los checks de la PR 12 y dime qué falla
```

Qué NO debe hacer sin tu aprobación:

- Crear PRs, comentar issues o hacer merge/push.
- Cerrar o reabrir issues.
- Tocar repos que no sean este.

Cómo probarlo:

1. `/mcps` → selecciona `github` → autoriza con tu cuenta (OAuth).
2. Pide `lista las issues abiertas` (solo lectura, sin riesgo).
3. Para escritura, pide primero el plan: `propón la PR pero no la crees`.

Autenticación: OAuth por defecto, sin tokens en el repo.
Para revocar: `opencode mcp logout github`.

### `context7` — docs que no alucinan

Responde con la documentación real y actualizada de una librería
en vez de tirar de memoria. Clave con Next 16 + React 19, que cambian rápido.

Qué puede hacer:

```text
¿Cómo se hace fetch de datos en un Server Component de Next 16?
¿Qué prop cambió en React 19 para este caso?
Dame el ejemplo oficial de Tailwind para un botón disabled accesible
```

Qué NO hace:

- No ejecuta código ni toca tu repo. Solo lectura de docs.
- No sustituye a `nextjs-patterns`: Context7 da la doc oficial,
  la skill da nuestro criterio de proyecto.

Cómo probarlo:

1. `/mcps` → comprueba `context7 connected`.
2. Pregunta algo versionable: `según Context7, cómo ... en Next 16`.
3. Si la respuesta no cita versión, pídele que la cite.

## Cómo ver estado y autenticar

```sh
opencode mcp list
```

- `connected` → listo.
- `needs authentication` → abre OpenCode, ejecuta `/mcps`,
  selecciona el servidor y completa el login en el navegador.
- `disconnected` → revisa la config y vuelve a listar.

## Cómo añadir un servidor nuevo

1. Añade la entrada en `.opencode/opencode.jsonc`, bajo `mcp.servers`:

```jsonc
{
  "mcp": {
    "servers": {
      "mi-server": {
        "type": "remote",
        "url": "https://mcp.ejemplo.com/mcp"
      }
    }
  }
}
```

2. Para un servidor local:

```jsonc
{
  "mcp": {
    "servers": {
      "mi-local": {
        "type": "local",
        "command": ["npx", "-y", "mi-paquete-mcp"]
      }
    }
  }
}
```

3. Guarda, ejecuta `opencode mcp list` y autentica con `/mcps` si lo pide.
4. Documenta el servidor en la tabla de arriba y en `AGENTS.md` si el agente
   debe usarlo de oficio.
5. Actualiza `MEMORY.md` con la decisión y el porqué.

Para desactivar sin borrar: pon `"disabled": true` en ese servidor.

## Seguridad mínima

- Secretos solo en variables de entorno (`{env:NOMBRE}`), nunca en el repo.
- Remotos con OAuth por defecto. Solo pon `oauth: false` + header con API key
  si el servidor no soporta OAuth, y con aprobación explícita.
- Acciones con efecto (crear PR, comentar, merge, navegar fuera de localhost)
  requieren propuesta previa y tu aprobación.
- Revisa las tools que expone un servidor nuevo antes de usarlo (`/mcps`).
- Figma NO está incluido por decisión actual (ver `MEMORY.md`).

## Relación con el resto del esqueleto

- `AGENTS.md` dice *cuándo* usar cada MCP y qué requiere aprobación.
- `MEMORY.md` guarda qué servidores están activos y porqué.
- Los comandos piden acciones, las skills aportan criterio, los MCP aportan
  herramientas externas.
