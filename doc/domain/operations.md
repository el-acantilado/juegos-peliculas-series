# Operaciones y recomendaciones

## Fuente autoritativa

Los archivos bajo `data/` son autoritativos. Las respuestas, perfiles y recomendaciones son vistas calculadas y no se guardan como hechos independientes.

## Vistas derivadas

### Perfil positivo por medio

Incluye señales de obras con experiencia suficiente y valoración 7–10. Da más peso a 9–10, peso positivo normal a 8 y peso débil o condicionado a 7.

Responde: qué características tienden a gustarle al usuario en juegos, películas o series.

### NO-perfil por medio

Incluye señales de obras con experiencia suficiente y valoración 1–5. La fuerza negativa aumenta al bajar la puntuación.

Responde: qué características, fricciones o combinaciones suelen causar rechazo.

### Zona ambivalente

La valoración 6 y las opiniones mixtas sirven para explicar límites y condiciones, pero no deben presentarse como gusto o rechazo fuerte.

### Candidatos pendientes

Agrupa obras `sin jugar` o `parcial` sin veredicto. Sirve como lista de exploración, con peso cero en el perfil.

### Vista multimedia

Compara rasgos de `detalles`, opiniones y fricciones que puedan tener sentido entre medios. Mantiene separados los perfiles base y explica cualquier inferencia transversal.

## Cálculos

### Fuerza de una señal

La valoración determina la dirección y fuerza inicial. La evidencia textual especifica qué rasgo recibe esa señal. No se atribuye la nota completa a todos los detalles indiscriminadamente.

### Confianza derivada

Se expresa al responder como alta, media o baja:

- Alta: experiencia suficiente, veredicto claro y razones específicas apoyadas por varias observaciones compatibles.
- Media: veredicto claro pero evidencia limitada, o patrón apoyado por pocas obras.
- Baja: experiencia parcial, lenguaje tentativo, identidad dudosa o señal aislada.

La confianza no es una opinión adicional del usuario ni un campo persistente.

### Recomendación

Una recomendación debe ponderar:

1. Coincidencias con el perfil positivo del medio.
2. Conflictos con el NO-perfil.
3. Fricciones conocidas.
4. Intensidad de las obras que sustentan cada patrón.
5. Confianza y datos faltantes.
6. En juegos, ritmo y respuesta de la interacción cuando sean relevantes.

La salida debe explicar por qué podría funcionar, qué riesgo concreto existe y cuánta confianza merece. No se reduce a contar etiquetas.

No hay monedas, unidades temporales ni reglas de redondeo aplicables. Las puntuaciones se conservan como enteros.

## Flujo para añadir o actualizar

1. Sincronizar y leer configuración, habilidad y registros relacionados.
2. Resolver identidad y buscar duplicados.
3. Registrar literalmente el veredicto y sus matices.
4. Aplicar una valoración solo si fue dada o si el usuario aprobó explícitamente una conversión.
5. Omitir campos desconocidos.
6. Validar el esquema.
7. Mutar un archivo mediante Atlas.
8. Verificar estado limpio y publicado.

## Flujo para recomendar

1. Determinar el medio solicitado o si la consulta es multimedia.
2. Leer obras positivas, negativas, ambivalentes y reglas generales relevantes.
3. Separar hechos conocidos de inferencias.
4. Contrastar candidatos con perfil y NO-perfil.
5. Explicar coincidencias, riesgos y confianza.
6. No guardar la consulta ni su respuesta salvo petición expresa.

## Importaciones, exportaciones y automatización

- Importaciones masivas: no aplicable por ahora; el seed aprobado se carga como registros normales.
- Exportaciones: no aplicable por ahora; Markdown y Git ya son portables.
- Dashboards: no aplicable a la escala actual.
- Recordatorios: no aplicable.
- Procesos recurrentes: no hay ninguno.
- Índices generados: no hay ninguno; si aparecen, se ubican en `bin/indexes/` y se regeneran conforme a `indexing.md`.
