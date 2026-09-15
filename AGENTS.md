# Reglas del proyecto

Este repositorio es un proyecto hijo de Atlas Automata.

Antes de razonar o modificar la biblioteca:

1. Ejecuta `atlas_sync` (o `.atlas/bin/atlas-mcp --root <repo> --sync` si la herramienta MCP no está disponible).
2. Lee `AUTOMATIZER.md`, `doc/modelo-biblioteca.md` y las habilidades aplicables bajo `ai/skills/`.
3. Lee los registros existentes bajo `data/` antes de proponer cambios.

`AUTOMATIZER.md` y todo archivo bajo `data/`, `doc/`, `ai/` o `log/` son estado protegido. Léelos directamente, pero modifícalos solo mediante `atlas_create`, `atlas_update`, `atlas_delete` o `atlas_move`.

Usa siempre fusiones Git; nunca rebase ni push forzado. Detente y comunica cualquier conflicto sin resolverlo silenciosamente.

Atlas Automata está fijado como submódulo en `lib/atlas-automata`.

<!-- atlas-automata:start -->
## Atlas Automata

Start every user request by calling `atlas_sync` and `atlas_status`.

If `atlas_status` reports `setup` other than `complete`, load `ai/skills/configure/SKILL.md` and conduct its complete agent-led configuration before accepting or writing domain data. Do not skip a phase, silently choose a semantic default, or ask the user to design the repository unaided.

Read `AUTOMATIZER.md`, relevant documentation, installed skills, and existing data before reasoning about a mutation. `AUTOMATIZER.md` and files under `data/`, `doc/`, `ai/`, and `log/` are protected: read them directly, but write them only with `atlas_create`, `atlas_update`, `atlas_delete`, or `atlas_move`.

Use merge-only Git synchronization. Never rebase, force-push, silently resolve a conflict, or silently reinterpret historical information.
<!-- atlas-automata:end -->
