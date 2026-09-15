# Biblioteca personal

Este repositorio conserva los juegos, las películas y las series que le gustan a su propietario.

## Alcance

- Colecciones: juegos, películas y series.
- Cada obra se registra en un archivo Markdown independiente dentro de `data/juegos/`, `data/peliculas/` o `data/series/`.
- La biblioteca comienza vacía: no se añade ninguna obra sin que el usuario la indique.
- Los registros conservan tanto hechos objetivos como la valoración personal del usuario.

## Principios

- No inventar títulos, valoraciones, fechas ni plataformas.
- Mantener el título original y, cuando sea útil, el título usado en español.
- Distinguir siempre entre estado de consumo y valoración.
- Admitir información incompleta; usar `desconocido` solo cuando sea necesario y no pueda dejarse el campo vacío.
- Evitar duplicados comparando tipo, título original y año.
- Conservar cambios históricos y aclarar ambigüedades antes de reinterpretar datos.

## Operaciones habituales

- Añadir una obra favorita.
- Corregir o completar sus metadatos.
- Cambiar el estado o la valoración personal.
- Consultar y filtrar la colección por tipo, estado, género, año, plataforma o etiquetas.
