# Reglas del proyecto

Este repositorio es un proyecto hijo de Atlas Automata.

Antes de razonar o modificar la biblioteca:

1. Ejecuta `atlas_sync` (o `.atlas/bin/atlas-mcp --root <repo> --sync` si la herramienta MCP no está disponible).
2. Lee `AUTOMATIZER.md`, `doc/modelo-biblioteca.md` y las habilidades aplicables bajo `ai/skills/`.
3. Lee los registros existentes bajo `data/` antes de proponer cambios.

`AUTOMATIZER.md` y todo archivo bajo `data/`, `doc/`, `ai/` o `log/` son estado protegido. Léelos directamente, pero modifícalos solo mediante `atlas_create`, `atlas_update`, `atlas_delete` o `atlas_move`.

Usa siempre fusiones Git; nunca rebase ni push forzado. Detente y comunica cualquier conflicto sin resolverlo silenciosamente.

Atlas Automata está fijado como submódulo en `lib/atlas-automata`.
