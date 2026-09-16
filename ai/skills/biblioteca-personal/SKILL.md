---
name: biblioteca-personal
description: Gestionar, consultar y usar para recomendaciones la biblioteca personal de juegos, películas y series.
---

# Biblioteca personal de recomendaciones

Usa esta habilidad cuando el usuario quiera añadir, editar, eliminar, consultar o comparar obras, construir su perfil o NO-perfil, o recibir recomendaciones.

## Antes de actuar

1. Ejecuta `atlas_sync` y `atlas_status`.
2. Si el setup no está completo, aplica íntegramente `configure` antes de escribir datos.
3. Lee `AUTOMATIZER.md`, `doc/domain/model.md`, `doc/domain/indexing.md` y `doc/domain/operations.md`.
4. Lee los registros relacionados bajo `data/`, incluidos perfiles generales.
5. Busca duplicados y resuelve identidades ambiguas antes de mutar.

## Escritura protegida

Toda escritura en `AUTOMATIZER.md`, `data/`, `doc/`, `ai/` o `log/` se hace exclusivamente mediante `atlas_create`, `atlas_update`, `atlas_delete` o `atlas_move`.

Cada mutación solicitada cambia un registro y lleva un resumen semántico. Atlas puede actualizar además los `index.md` administrados de las carpetas afectadas dentro del mismo commit. Nunca edites esos índices directamente ni reinterpretes datos históricos silenciosamente.

## Registro de obras

- Guarda un archivo por obra bajo `data/<medio>/<particion>/`.
- Usa `positivos` para 7–10, `mixtos` para 6, `negativos` para 1–5 y `pendientes` cuando no hay valoración.
- Si cambia la banda, usa `atlas_move`; nunca copies el registro.
- Sigue el esquema documentado y omite campos opcionales desconocidos.
- Conserva el lenguaje y los matices del usuario.
- No inventes puntuaciones, experiencia, rejugabilidad, metadatos ni razones.
- Solo aplica conversiones cualitativas a números cuando el usuario haya aprobado el mapeo.
- Un pendiente puede registrarse sin valoración y no pesa en el perfil.
- En juegos, resume mecánicas, dificultad, ritmo, controles y estructura dentro de `jugabilidad`.
- Usa `positivo`, `negativo`, `fricciones` y `detalles` según su semántica; no añadas campos ad hoc si uno existente basta.
- Una edición o plataforma no duplica la obra salvo que represente una experiencia que el usuario quiera valorar por separado.

## Reglas generales

Guarda en `data/perfil/` las preferencias declaradas que abarcan varias obras. Una regla general puede contener:

- ámbito;
- preferencia;
- condiciones o matices;
- ejemplos aportados;
- consecuencias para recomendaciones.

No copies la misma regla completa en cada obra relacionada.

## Consultas de perfil

- Separa juegos, películas y series.
- Perfil positivo: valoraciones 7–10, graduadas según la escala.
- NO-perfil: valoraciones 1–5, con mayor señal negativa cuanto más baja la nota.
- Valoración 6: evidencia ambivalente.
- Registros sin veredicto: peso cero.
- Calcula confianza a partir de experiencia, claridad y cantidad de evidencia; no la presentes como dato aportado por el usuario.
- Fundamenta cada patrón con obras concretas y señala excepciones.

## Recomendaciones

1. Lee tanto el perfil positivo como el NO-perfil del medio.
2. Busca coincidencias, conflictos y fricciones; no te limites a géneros.
3. En juegos, presta atención a ritmo, respuesta, repetición, espera, RNG y variedad cuando la evidencia los haga relevantes.
4. Para consultas multimedia usa rasgos comparables de `detalles`, manteniendo explícitas las diferencias entre medios.
5. Explica por qué la recomendación podría encajar, los riesgos y la confianza.
6. Distingue datos conocidos de inferencias y verifica información externa cambiante cuando sea necesaria.
7. No alteres la biblioteca durante una consulta salvo que el usuario también solicite guardar algo.

## Validación final

Después de mutar:

- comprueba que el archivo cumple el modelo y está en la partición correcta;
- comprueba que los `index.md` de la ruta enlazan el registro;
- vuelve a ejecutar `atlas_status`;
- confirma que Git está limpio y publicado;
- informa exactamente qué cambió.
