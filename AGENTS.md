# Reglas del proyecto

Este repositorio es un proyecto hijo de Atlas Automata.

Al iniciar una sesión de trabajo con la biblioteca:

1. Ejecuta una sola vez `atlas_sync` (o `.atlas/bin/atlas-mcp --root <repo> --sync` si la herramienta MCP no está disponible) y después `atlas_status`.
2. No repitas `atlas_sync` para cada solicitud de la misma sesión; las mutaciones protegidas sincronizan internamente.
3. Lee `AUTOMATIZER.md`, `doc/modelo-biblioteca.md` y las habilidades aplicables bajo `ai/skills/`.
4. Lee los registros existentes bajo `data/` antes de proponer cambios.

`AUTOMATIZER.md` y todo archivo bajo `data/`, `doc/`, `ai/` o `log/` son estado protegido. Léelos directamente, pero modifícalos solo mediante `atlas_create`, `atlas_update`, `atlas_delete` o `atlas_move`.

Usa siempre fusiones Git; nunca rebase ni push forzado. Detente y comunica cualquier conflicto sin resolverlo silenciosamente.

Atlas Automata está fijado como submódulo en `lib/atlas-automata`.

<!-- atlas-automata:start -->
## Atlas Automata

At the start of an agent session, call `atlas_sync` once and then call `atlas_status`. Do not repeat `atlas_sync` for every user request in the same session; protected mutation tools synchronize internally.

Every user request concerning the configured domain is domain work, even when phrased as casual conversation. Before answering, load the relevant discovered skill and existing records. Treat new facts, preferences, ratings, corrections, and decisions supplied by the user as candidate domain mutations; preserve them through Atlas MCP when they belong in the configured domain.

If `atlas_status` reports `setup` other than `complete`, load `ai/skills/configure/SKILL.md` and conduct its complete agent-led configuration before accepting or writing domain data. Do not skip a phase, silently choose a semantic default, or ask the user to design the repository unaided.

Read `AUTOMATIZER.md`, relevant documentation, installed skills, and existing data before reasoning about a mutation. `AUTOMATIZER.md` and files under `data/`, `doc/`, `ai/`, and `log/` are protected: read them directly, but write them only with `atlas_create`, `atlas_update`, `atlas_delete`, or `atlas_move`.

Use merge-only Git synchronization. Never rebase, force-push, silently resolve a conflict, or silently reinterpret historical information.
<!-- atlas-automata:end -->
