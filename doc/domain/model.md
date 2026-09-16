# Modelo de la biblioteca

## Organización

Cada obra ocupa un archivo Markdown:

- `data/juegos/<slug>.md`
- `data/peliculas/<slug>.md`
- `data/series/<slug>.md`

El `slug` se deriva del título original en minúsculas, sin tildes y con palabras separadas por guiones. Si dos obras del mismo tipo coinciden, se añade el año.

## Metadatos

Cada archivo comienza con YAML front matter. Campos comunes:

```yaml
---
tipo: juego | pelicula | serie
titulo: Título usado por el usuario
titulo_original: Título original
anio: 2024
estado: pendiente | en_curso | completado | abandonado
valoracion: 1-10
generos:
  - genero
plataformas:
  - plataforma, formato o servicio
etiquetas:
  - etiqueta personal
fecha_agregado: YYYY-MM-DD
---
```

Reglas:

- `tipo`, `titulo` y `fecha_agregado` son obligatorios.
- Los demás campos son opcionales y deben omitirse cuando no se conozcan.
- `valoracion` es un entero de 1 a 10 y expresa gusto personal, no una nota externa.
- `estado` describe la relación actual del usuario con la obra; no implica que haya dejado de gustarle.
- `plataformas` puede representar hardware o tienda en juegos, y formato o servicio de visualización en películas y series.
- Los géneros y las etiquetas se escriben en minúsculas salvo nombres propios.
- Una misma obra no se duplica por estar disponible en varias plataformas.

## Contenido narrativo

Después del front matter se pueden usar estas secciones, omitiendo las vacías:

```markdown
# Título

## Por qué me gusta

Texto libre con la razón personal.

## Notas

Observaciones, recuerdos, recomendaciones o contexto.
```

No convertir una opinión del usuario en hecho objetivo. Las citas textuales del usuario pueden conservarse en “Por qué me gusta”.

## Datos específicos

Cuando el usuario los aporte o sea útil registrarlos:

- Juego: `desarrollador`, `editor`, `fecha_lanzamiento`.
- Película: `direccion`, `duracion_minutos`, `fecha_estreno`.
- Serie: `creacion`, `temporadas`, `episodios`, `fecha_estreno`, `fecha_final`.

## Identidad y duplicados

Antes de crear un registro, comparar el tipo, el título original y el año. Títulos alternativos y traducciones pertenecen al mismo registro. Si la identidad sigue siendo ambigua, preguntar antes de crear o fusionar información.
