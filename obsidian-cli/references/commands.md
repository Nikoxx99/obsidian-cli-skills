# Obsidian CLI Reference

Fuente principal: https://help.obsidian.md/cli

## Estado y requisitos

- El CLI de Obsidian aparece como feature en estado early access en la documentacion oficial.
- Se requiere una version reciente de Obsidian Desktop con CLI disponible y acceso al vault objetivo.
- Validar instalacion con:
```bash
obsidian version
obsidian help
```

## Sintaxis clave

- Forma general: `obsidian <command> [parameter=value] [flags]`
- Parametros con espacios: usar comillas (`query="mi texto"`).
- Flags booleanos: sin valor (`silent`, `overwrite`, `copy`, `json` segun comando).
- Texto multilinea: usar secuencias como `\n` y `\t`.
- El comando sin argumentos abre la UI en modo interactivo.

## Targeting de vault y archivo

- `vault=<name>`: fuerza el vault sobre el que operar.
- `file=<name>`: nota por nombre.
- `path=<path>`: ruta de archivo desde la raiz del vault (preferido si hay ambiguedad).

## Grupos de comandos (resumen)

- Ayuda/inspeccion: `help`, `version`, `status`, `vault`, `vaults`.
- Notas: `create`, `read`, `open`, `append`, `prepend`, `replace`, `rename`, `move`, `delete`.
- Daily notes: `daily`, `daily:read`, `daily:append`, `daily:prepend`, `daily:open`.
- Busqueda y organizacion: `search`, `tasks`, `tags`, `outline`, `links`, `backlinks`.
- Metadatos y propiedades: `properties`, `property`, `property:set`, `property:delete`.
- Plantillas y comandos de app: `templates`, `template:*`, `commands`, `command`.
- Integraciones de Obsidian: `publish:*`, `sync:*`.
- Desarrollo y plugins: `plugin:*`, `dev:*`, `theme:*`.

## Flujos rapidos

Crear nota, leerla y agregar una tarea:
```bash
obsidian create name="Plan semanal" content="# Plan semanal\n\nObjetivos:"
obsidian read file="Plan semanal"
obsidian append file="Plan semanal" content="\n- [ ] Revisar pendientes"
```

Buscar notas y devolver JSON:
```bash
obsidian search query="retro" format=json limit=10
```

Usar daily note para log:
```bash
obsidian daily:append content="- Deploy realizado"
obsidian daily:read
```

## Buenas practicas

- Confirmar `vault` y `path` antes de mutaciones (`delete`, `move`, `replace`).
- Preferir salidas estructuradas (`format=json`) cuando otra herramienta consumira el resultado.
- Limitar alcance con `limit` y filtros para evitar respuestas excesivas.
- Si una accion no es clara por nombre de archivo duplicado, pasar a `path=`.
