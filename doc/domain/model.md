# Modelo del sistema de recomendaciones

## Entidades y ciclo de vida

Hay tres colecciones independientes: juegos, películas y series. Cada archivo representa una obra y la evaluación vigente del usuario, no una sesión ni un evento. Dentro de cada medio, la carpeta `positivos`, `mixtos`, `negativos` o `pendientes` expresa la función recomendadora de la valoración.

Un registro se crea cuando el usuario aporta una opinión o quiere conservar una obra pendiente. Se actualiza cuando cambia o se precisa el veredicto. No hay estados administrativos de archivo. Solo se elimina cuando el usuario lo solicita o se confirma un duplicado; Git conserva el historial.

Las obras pendientes pueden registrarse, pero no aportan evidencia al perfil hasta que exista una valoración sustentada por experiencia suficiente. Cuando cambia la banda de valoración, el mismo registro se mueve a la partición correspondiente; no se crea una copia.

## Esquema común

Los registros son Markdown con front matter YAML:

```yaml
---
tipo: juego | pelicula | serie
titulo: Título usado por el usuario
titulo_original: Solo si difiere
año: 2024
valoracion: 1
experiencia: jugado | parcial | sin jugar
repetiria: sí | quizá | no
opinion: Resumen libre
positivo:
  - rasgo
negativo:
  - rasgo
fricciones:
  - rasgo
detalles:
  - rasgo compartido o contexto útil
---
```

Campos requeridos:

- `tipo`
- `titulo`
- `experiencia`

Campos opcionales, que se omiten si no fueron aportados o verificados:

- `titulo_original`
- `año`
- `valoracion`
- `repetiria`
- `opinion`
- `positivo`
- `negativo`
- `fricciones`
- `detalles`

No se usa `desconocido` como relleno.

## Campo exclusivo de juegos

```yaml
jugabilidad: Resumen de mecánicas, controles, dificultad, ritmo, respuesta, estructura, progresión, combate o exploración
```

`jugabilidad` es texto libre y resume lo relevante de jugar la obra. Películas y series no tienen campos adicionales fijos. Sus aspectos narrativos o experienciales se expresan en `detalles`, `positivo`, `negativo`, `fricciones` u `opinion`.

## Escala de valoración

- 10: Favorito personal.
- 9: Excelente.
- 8: Muy buena experiencia única; valió claramente la pena aunque no sea necesario repetirla.
- 7: Bueno con fallas.
- 6: Regular o mixto.
- 5: Mediocre.
- 4: Malo.
- 3: Pésimo.
- 2: Terrible.
- 1: Detestable o incompatible.

Para el cálculo del perfil:

- 9–10: evidencia positiva fuerte.
- 8: evidencia positiva, sin asumir rejugabilidad.
- 7: evidencia positiva débil o condicionada.
- 6: neutral o ambivalente.
- 1–5: evidencia negativa, con fuerza creciente al bajar la puntuación.

## Experiencia y datos ausentes

- `jugado`: hubo experiencia suficiente para emitir el veredicto registrado; no implica necesariamente haber terminado el juego.
- `parcial`: la exposición fue escasa o el veredicto continúa abierto.
- `sin jugar`: no hubo experiencia directa.
- Los registros `parcial` sin veredicto y `sin jugar` no alteran los perfiles.
- No se infiere `repetiria`; se omite si el usuario no lo indicó.
- No se fuerza una valoración cuando el usuario solo declara algo pendiente.
- La confianza no se almacena. Se deriva al consultar: aumenta con experiencia suficiente y explicaciones concretas; disminuye con experiencia parcial, ambigüedad o falta de razones.

## Taxonomía semántica

- `positivo`: rasgos que elevaron la experiencia.
- `negativo`: rasgos evaluados desfavorablemente.
- `fricciones`: elementos que dificultan disfrutar la obra, incluso si no son defectos universales.
- `detalles`: contexto, rasgos comparables y puentes entre medios.
- `jugabilidad`: síntesis específica del acto de jugar.

Los valores son frases breves en español. Se reutiliza la misma formulación cuando el significado sea realmente equivalente, pero no se obliga al usuario a elegir de una lista cerrada.

## Relaciones y perfiles

Cada obra aporta señales a un perfil positivo o a un NO-perfil de su propio medio según su valoración, experiencia y explicación. Las consultas multimedia comparan `detalles` y otros rasgos semánticamente compatibles, pero conservan las diferencias entre medios.

Los perfiles se guardan exclusivamente en cuatro archivos bajo `data/perfil/`: `juegos.md`, `peliculas.md`, `series.md` y `general.md`. Cada perfil de medio concentra sus reglas declaradas y evidencia transversal de ese medio. `general.md` concentra estilos visuales y otros rasgos comparables entre medios. No se crean archivos de regla individuales.

## Identidad y validación

La identidad estable es `tipo + titulo_original normalizado + año` cuando esos datos existen. Si falta el original o el año, se usa el título aportado y se conserva la incertidumbre.

Antes de crear:

1. Buscar el título, variantes ortográficas y títulos alternativos dentro de la colección.
2. Comprobar año o edición si podrían existir homónimos o remakes.
3. Preguntar si la identidad sigue siendo ambigua.
4. No fusionar ediciones con valoraciones materialmente distintas sin confirmación.

Validaciones:

- `tipo` debe coincidir con la carpeta del medio.
- La ruta debe coincidir con la banda: 7–10 en `positivos`, 6 en `mixtos`, 1–5 en `negativos` y ausencia de valoración en `pendientes`.
- `valoracion` debe ser un entero de 1 a 10.
- `experiencia` usa únicamente los tres valores definidos.
- Una obra sin experiencia suficiente puede omitir `valoracion`.
- No se convierten opiniones personales en hechos objetivos.
