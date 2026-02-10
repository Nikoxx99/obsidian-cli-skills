---
name: obsidian-cli
description: Operar Obsidian desde terminal con Obsidian CLI para automatizar flujos sobre vaults y notas Markdown. Usar cuando se necesite crear, leer, modificar, mover o eliminar notas; buscar contenido; trabajar con daily notes, tareas, propiedades, enlaces, plantillas, publish o sync; ejecutar comandos de desarrollo de plugins/temas; o integrar Obsidian en scripts y pipelines.
---

# Obsidian CLI

## Resumen

Usar esta skill para ejecutar tareas en Obsidian desde terminal de forma reproducible y segura. Resolver solicitudes de automatizacion con comandos concretos, validaciones previas y salida util para scripting.

## Flujo de trabajo

1. Confirmar contexto operativo:
- Verificar que Obsidian este instalado, actualizado y con CLI habilitado.
- Verificar vault objetivo (`cwd`, vault activo o `vault=<name>`).
- Verificar objetivo de archivo (`file=<name>` o `path=<path>`), evitando ambiguedad.

2. Elegir estrategia:
- Una sola accion: ejecutar comando puntual (`obsidian <command>`).
- Flujo guiado: abrir TUI con `obsidian` y encadenar operaciones.
- Automatizacion: generar secuencia de comandos con parametros explicitos.

3. Ejecutar con parametros robustos:
- Usar `parameter=value` y comillas si hay espacios.
- Usar flags booleanos sin valor (`silent`, `overwrite`, etc.).
- Para contenido multilinea, usar `\n` y `\t`.

4. Validar y devolver resultado:
- Confirmar cambios hechos (archivo creado/modificado, conteos, estado).
- Incluir salida en formato util para el caso (`text` o `json` si aplica).
- Ofrecer siguiente comando natural para continuar el flujo.

## Patrones de ejecucion

`Vault y archivo`
- Preferir `path=<ruta-desde-raiz-del-vault>` cuando exista riesgo de colision por nombre.
- Usar `file=<nombre>` solo si la resolucion es inequivoca.
- Si se trabaja fuera del vault en `cwd`, fijar `vault=<name>`.

`Lectura y escritura de notas`
- Leer: `read`, `daily:read`, `template:read`, `sync:read`.
- Escribir: `create`, `append`, `prepend`, `daily:append`, `daily:prepend`.
- Mutaciones destructivas: confirmar destino antes de `delete` o `move`.

`Busqueda y analisis`
- Buscar texto con `search query=...` y usar `format=json` para integraciones.
- Extraer estructura con `outline`, enlaces con `backlinks` y `links`.

`Automatizacion y desarrollo`
- Ejecutar comandos de app/plugin con `command id=...` y listar con `commands`.
- Para debugging de plugins/temas, usar comandos `dev:*` y `plugin:*`.

## Comandos base recomendados

- Inspeccion inicial:
```bash
obsidian help
obsidian version
obsidian vault
```

- Operaciones de nota:
```bash
obsidian create name="Nota de prueba" content="# Titulo\n\nContenido"
obsidian read file="Nota de prueba"
obsidian append file="Nota de prueba" content="- [ ] Siguiente accion"
```

- Busqueda y resumen:
```bash
obsidian search query="proyecto alpha" format=json limit=20
obsidian tags counts
obsidian tasks daily
```

- Copiar salida a portapapeles:
```bash
obsidian read --copy
```

## Referencias

Consultar `references/commands.md` para:
- Resumen de comandos por categoria.
- Requisitos actuales de version y estado de early access.
- Reglas de parametros, flags y targeting de vault/archivo.
- Ejemplos listos para copiar en flujos de automatizacion.

## Criterios de calidad

- Priorizar comandos idempotentes cuando sea posible.
- Mostrar siempre el comando exacto antes de cambios destructivos.
- Preferir `format=json` en salidas destinadas a herramientas externas.
- Si el comando falla, devolver causa probable y siguiente intento concreto.
