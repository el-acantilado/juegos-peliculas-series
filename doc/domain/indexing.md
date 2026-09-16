# Identidad, partición e índices

## Accesos esperados

El sistema debe poder:

- Encontrar una obra por título o variante.
- Navegar por medio y por función recomendadora.
- Separar inmediatamente perfil positivo, zona mixta, NO-perfil y pendientes.
- Filtrar y ordenar por valoración y experiencia.
- Buscar texto en opinión, positivo, negativo, fricciones, detalles y jugabilidad.
- Comparar rasgos entre juegos, películas y series sin confundir sus perfiles.
- Detectar duplicados aunque los registros estén en particiones distintas.

## Identidad y duplicados

La clave conceptual es:

`tipo + título original normalizado + año`

Cuando falten título original o año, se usa el título conocido y se pregunta ante posibles colisiones. Diferentes plataformas no crean registros distintos. Un remake sí es una obra distinta. Una edición se separa únicamente si el usuario quiere conservar valoraciones materialmente diferentes.

Antes de crear o mover un registro se buscan, sin distinguir mayúsculas ni tildes:

- título principal;
- título original;
- slug;
- año, edición o plataforma cuando desambigüen;
- coincidencias en todas las particiones del mismo medio.

## Árbol físico aprobado

```text
data/
├── index.md
├── juegos/
│   ├── index.md
│   ├── positivos/
│   ├── mixtos/
│   ├── negativos/
│   └── pendientes/
├── peliculas/
│   ├── index.md
│   ├── positivos/
│   ├── mixtos/
│   ├── negativos/
│   └── pendientes/
├── series/
│   ├── index.md
│   ├── positivos/
│   ├── mixtos/
│   ├── negativos/
│   └── pendientes/
└── perfil/
    ├── index.md
    ├── juegos.md
    ├── peliculas.md
    ├── series.md
    └── general.md
```

Git no conserva carpetas vacías. Por eso las carpetas de películas o series aparecerán cuando reciban su primer registro; desde ese momento Atlas creará también su `index.md`.

## Regla de partición

- `positivos/`: valoración 7–10.
- `mixtos/`: valoración 6.
- `negativos/`: valoración 1–5.
- `pendientes/`: sin valoración, normalmente con experiencia parcial o sin experimentar.
- `data/perfil/juegos.md`: perfil único de juegos.
- `data/perfil/peliculas.md`: perfil único de películas.
- `data/perfil/series.md`: perfil único de series.
- `data/perfil/general.md`: estilos visuales y rasgos transversales.

Si una valoración cambia de banda, el registro se mueve mediante `atlas_move`. No se copia ni se duplica.

## Rutas canónicas

- `data/juegos/<particion>/<slug>.md`
- `data/peliculas/<particion>/<slug>.md`
- `data/series/<particion>/<slug>.md`
- `data/perfil/juegos.md`
- `data/perfil/peliculas.md`
- `data/perfil/series.md`
- `data/perfil/general.md`

El slug se deriva del título original si existe; de lo contrario, del título usado por el usuario. Se escribe en minúsculas ASCII, usa guiones entre palabras y elimina signos. Si hay colisión, se añade el año o una edición breve.

Ejemplos:

- `data/juegos/positivos/goldeneye-007.md`
- `data/juegos/negativos/dishonored.md`
- `data/juegos/pendientes/system-shock-remake.md`
- `data/perfil/juegos.md`

## Índices de carpeta

Atlas MCP reserva y mantiene automáticamente un `index.md` en cada carpeta existente bajo `data/`.

Cada índice:

- enlaza únicamente las subcarpetas y registros inmediatos;
- se actualiza en el mismo commit que una creación, movimiento o eliminación;
- se ordena de forma determinista;
- no contiene hechos de dominio independientes;
- no se edita manualmente mediante Atlas.

Los registros de obras y reglas de perfil siguen siendo la fuente autoritativa. Los `index.md` son navegación reproducible dentro de `data/`.

## Índices adicionales

No se requieren índices adicionales ni `bin/indexes/`. La partición física y los índices de carpeta responden a las consultas previstas sin duplicar datos.
