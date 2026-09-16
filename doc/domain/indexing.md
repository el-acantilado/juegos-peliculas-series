# Identidad, rutas e indexación

## Accesos esperados

El sistema debe poder:

- Encontrar una obra por título o variante.
- Filtrar y ordenar por medio, valoración y experiencia.
- Buscar texto en opinión, aspectos positivos, negativos, fricciones, detalles y jugabilidad.
- Separar señales del perfil positivo y del NO-perfil.
- Explicar por qué una obra puede gustar o no.
- Comparar rasgos entre juegos, películas y series sin confundir sus perfiles.
- Mantener candidatos pendientes sin que influyan en recomendaciones.

La escala prevista es personal y pequeña o mediana. La lectura directa de Markdown es suficiente.

## Identidad y duplicados

La clave conceptual es:

`tipo + título original normalizado + año`

Cuando falten título original o año, se usa el título conocido y se pregunta ante posibles colisiones. Diferentes plataformas no crean registros distintos. Un remake sí es una obra distinta. Una edición se separa únicamente si el usuario quiere conservar valoraciones materialmente diferentes.

La detección de duplicados compara, sin distinguir mayúsculas ni tildes:

- título principal;
- título original;
- slug;
- año, edición o plataforma cuando desambigüen.

## Rutas canónicas

- `data/juegos/<slug>.md`
- `data/peliculas/<slug>.md`
- `data/series/<slug>.md`
- `data/perfil/<slug>.md` para reglas generales declaradas por el usuario.

El slug se deriva del título original si existe; de lo contrario, del título usado por el usuario. Se escribe en minúsculas ASCII, reemplaza separadores por guiones y elimina signos. Si hay colisión, se añade el año o una edición breve.

Ejemplos:

- `data/juegos/goldeneye-007.md`
- `data/juegos/system-shock-remake.md`
- `data/perfil/aventuras-graficas.md`

## Organización física

Cada obra ocupa un archivo. La carpeta representa el tipo. No se replica el registro en carpetas de favoritos, pendientes o descartados; esas vistas se calculan mediante filtros.

Los archivos de `data/perfil/` almacenan reglas generales que no pertenecen a una sola obra y que ayudan a interpretar recomendaciones.

## Autoridad e índices

Los registros bajo `data/` son la única fuente autoritativa. No existe un índice manual con copias de títulos, puntuaciones o rasgos.

Por ahora no se genera ningún índice porque la escala no lo justifica. Las consultas usan búsqueda de archivos y texto. Si el volumen futuro lo exige, los índices reproducibles deberán escribirse bajo `bin/indexes/`, nunca bajo `data/`.

## Reconstrucción futura

Cualquier índice futuro deberá:

1. Eliminar y reconstruir únicamente su salida conocida bajo `bin/indexes/`.
2. Leer todos los registros válidos de `data/`.
3. Ordenar de forma determinista por tipo, título normalizado y ruta.
4. Incluir en su cabecera el comando exacto de reconstrucción.
5. No introducir información que no exista en las fuentes.
6. Poder regenerarse sin modificar archivos protegidos.

Como hoy no hay script ni índice generado, la reconstrucción es no aplicable.
