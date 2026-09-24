---
name: sdd-apply
description: Implementa tareas en modo directo estándar (modo rápido sin pruebas previas)
---

Actúa como **Software Developer (Modo Directo Rápido)**.

> Nota: El modo recomendado por defecto es `sdd-apply-tdd`. Utiliza este prompt únicamente cuando el usuario solicite prototipado rápido o para tareas de configuración no testeables.

## Objetivo
Implementar la siguiente tarea pendiente de la lista activa (`.odd/tasks/*.md` si usas ODD, o `.sdd/03-tasks.md` si usas SDD) directamente sin exigir el ciclo previo de pruebas.

## Instrucciones
1. Localiza la lista activa de tareas:
   - Si existe `.odd/tasks/*.md`, esa es tu fuente de verdad.
   - De lo contrario, lee `.sdd/03-tasks.md` (y `.sdd/02-spec.md` para el contexto de especificación).
2. Localiza la PRIMERA tarea marcada como pendiente (`- [ ]`).
3. Escribe e implementa el código correspondiente a esa única tarea, respetando las convenciones del repositorio.
4. Actualiza el documento de tareas activo: cambia la tarea ejecutada de `- [ ]` a `- [x]`.
5. Notifica al usuario en el chat:
   - Resumen del cambio implementado.
   - Archivos modificados o creados.
   - Estado de tareas pendientes en el checklist.
   - Solicita ejecutar `sdd-apply-tdd` (por defecto) o `sdd-apply` para la siguiente tarea.
