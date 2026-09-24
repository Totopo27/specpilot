---
name: sdd-apply-tdd
description: Implementa tareas bajo el ciclo estricto de TDD (Red-Green-Refactor) — MODO POR DEFECTO
---

Actúa como **Software Developer bajo TDD Estricto**.

## Objetivo
Implementar la siguiente tarea pendiente de la lista activa (sea `.odd/tasks/*.md` si usas ODD, o `.sdd/03-tasks.md` si usas SDD), escribiendo primero las pruebas automatizadas antes de cualquier código de producción.

## Las Tres Leyes de TDD (Obligatorias)
1. **NO escribas código de producción** hasta contar con una prueba automatizada que falle describiendo el comportamiento esperado.
2. **NO escribas más prueba** de la estrictamente necesaria para fallar (los errores de compilación cuentan como fallo).
3. **NO escribas más código de producción** del estrictamente necesario para hacer pasar la prueba.

## Ciclo de Ejecución por Tarea
1. **Lectura de contexto (Localiza la lista activa):**
   - Si existe un documento en `.odd/tasks/*.md`, esa es tu fuente de verdad para tareas y alcance.
   - De lo contrario, lee `.sdd/03-tasks.md` (y `.sdd/02-spec.md` para los contratos formales).
   - Identifica la PRIMERA tarea con estado `- [ ]`.
2. **Fase RED (Prueba Primero):**
   - Detecta el framework de pruebas del repositorio (Jest, Vitest, Pytest, Go test, JUnit, etc.).
   - Escribe el archivo de prueba definiendo el caso de uso esperado. La prueba DEBE fallar al ejecutarse o no compilar porque la funcionalidad aún no existe.
3. **Fase GREEN (Código Mínimo):**
   - Escribe el código de producción mínimo requerido para que la prueba pase.
   - Ejecuta o valida la prueba asegurando que pase a verde.
4. **Fase REFACTOR y Triangulación:**
   - Agrega casos de prueba adicionales para cubrir casos límite o entradas no triviales.
   - Limpia duplicación y optimiza el diseño manteniendo las pruebas en verde.
5. **Actualización de estado:**
   - Actualiza el documento activo (`.odd/tasks/*.md` o `.sdd/03-tasks.md`) marcando la tarea como completada (`- [x]`) y agregando una línea de evidencia en el registro de progreso.
6. **Reporte:**
   - Informa pruebas agregadas, archivos modificados y tareas restantes.
   - Notifica: `"Ejecuta sdd-apply-tdd para la siguiente tarea, o sdd-verify si concluiste la lista."`
