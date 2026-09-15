---
name: biblioteca-personal
description: Gestionar y consultar la biblioteca personal de juegos, películas y series de este repositorio.
---

# Biblioteca personal

Usa esta habilidad cuando el usuario quiera añadir, editar, eliminar, consultar, comparar u organizar juegos, películas o series que le gustan.

## Antes de actuar

1. Ejecuta `atlas_sync`.
2. Lee `AUTOMATIZER.md` y `doc/modelo-biblioteca.md`.
3. Busca registros existentes bajo `data/` antes de crear uno nuevo.
4. Si la identidad de la obra o la intención del usuario es ambigua, pregunta antes de mutar.

## Escritura

Toda escritura en `AUTOMATIZER.md`, `data/`, `doc/`, `ai/` o `log/` se hace exclusivamente con las herramientas Atlas:

- `atlas_create` para un registro nuevo.
- `atlas_update` para reemplazar el contenido completo de un registro.
- `atlas_delete` para eliminarlo cuando el usuario lo pida claramente.
- `atlas_move` para corregir su ruta o identidad.

Incluye siempre un resumen semántico breve. Una operación Atlas modifica un archivo protegido cada vez; realiza cambios relacionados de forma secuencial.

## Registro de obras

- Guarda un archivo por obra en la carpeta correspondiente a su tipo.
- Sigue exactamente el modelo documentado.
- Registra primero lo que el usuario afirma.
- No inventes valoraciones, estados, plataformas ni razones personales.
- Los metadatos objetivos pueden completarse solo cuando estén suficientemente verificados; distingue cualquier inferencia.
- Omite campos opcionales desconocidos.
- Conserva el lenguaje y los matices de la opinión del usuario.
- Antes de añadir una traducción o edición distinta, comprueba si pertenece a una obra ya registrada.

## Consultas

Lee directamente los archivos necesarios bajo `data/`. Explica los filtros aplicados y señala datos ausentes que puedan afectar el resultado. No alteres la biblioteca durante una consulta salvo que el usuario también pida guardar cambios.
