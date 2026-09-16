---
atlas_setup: in_progress
atlas_setup_version: 1
---

# Sistema personal de recomendaciones

## Propósito

Este repositorio conserva evidencia de gusto sobre juegos, películas y series para producir recomendaciones personales explicables. No pretende ser una base de datos enciclopédica.

## Usuario y lenguaje

- Usuario principal: propietario del repositorio.
- Visibilidad: pública; no se almacenará información sensible.
- Idioma de trabajo: español.
- Terminología preferida: `jugabilidad`, `positivo`, `negativo`, `fricciones` y `detalles`.

## Alcance

Incluye:

- Obras experimentadas que aportan evidencia al perfil positivo o al NO-perfil.
- Obras pendientes o apenas experimentadas como candidatas sin peso en el perfil.
- Opiniones, fricciones y detalles aportados por el usuario.
- Recomendaciones separadas para juegos, películas y series.
- Consultas multimedia basadas en rasgos comparables guardados en `detalles`.

Queda fuera:

- Catalogación exhaustiva de reparto, plataformas, servicios o metadatos externos.
- Historial de sesiones, progreso detallado y eventos de consumo.
- Puntuaciones de críticos o de otros usuarios.
- Automatizaciones externas, recordatorios y dashboards mientras no sean solicitados.

## Colecciones

- `data/juegos/`: un registro por videojuego.
- `data/peliculas/`: un registro por película.
- `data/series/`: un registro por serie.

Cada registro representa la evaluación vigente de una obra. Git conserva su historia. Las obras no se duplican por edición o plataforma salvo que el usuario quiera valorar experiencias materialmente distintas.

## Principios de recomendación

- El contenido de los registros es la fuente autoritativa.
- No se inventan puntuaciones, experiencias ni opiniones.
- Las valoraciones positivas y negativas tienen fuerza gradual.
- Una valoración 8 significa que la experiencia valió claramente la pena, aunque no exista deseo de repetirla.
- La confianza se calcula a partir del grado de experiencia y de la especificidad de la explicación; no se introduce manualmente.
- Los pendientes y las experiencias demasiado breves no alteran el perfil hasta tener veredicto.
- Las recomendaciones deben explicar coincidencias, conflictos, fricciones e incertidumbre.
- El perfil positivo y el NO-perfil se calculan por separado para juegos, películas y series.
- Las preguntas multimedia usan `detalles` como vocabulario compartido, sin mezclar automáticamente las preferencias propias de cada medio.

## Restricciones operativas

- Antes de cada solicitud se ejecutan `atlas_sync` y `atlas_status`.
- Los archivos protegidos se modifican únicamente mediante Atlas.
- La sincronización Git usa fusiones; nunca rebase ni push forzado.
- Los conflictos se comunican y no se resuelven silenciosamente.
- No existen índices autoritativos duplicados: las vistas se derivan de los registros.

## Configuración aprobada

- [x] Propósito, límites, privacidad y lenguaje.
- [x] Colecciones, ciclos de vida y relaciones.
- [x] Recuperación, identidad, rutas e indexación.
- [x] Esquema, taxonomía, validación y datos ausentes.
- [x] Vistas, cálculos y flujos operativos.
- [x] Compatibilidad con la configuración preliminar.
- [x] Propuesta final aprobada explícitamente.
- [ ] Artefactos persistidos y verificados.
