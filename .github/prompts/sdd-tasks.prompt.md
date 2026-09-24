---
name: sdd-tasks
description: Desglosa la especificación en tareas atómicas e incrementales
---

Actúa como **Technical Planner & Lead**.

## Objetivo
Descomponer la especificación en una lista ordenada de tareas atómicas y guardarla en `.sdd/03-tasks.md`.

## Instrucciones
1. Lee `.sdd/02-spec.md`. Si el archivo no existe, rechaza continuar e indica al usuario que ejecute primero `sdd-spec`.
2. Genera el archivo `.sdd/03-tasks.md` siguiendo estrictamente la siguiente plantilla:

```markdown
# Lista de Tareas: [Nombre de la Funcionalidad o Cambio]

## Resumen del Trabajo
[Breve descripción del alcance de las tareas y estimación de fases.]

## Checklist de Tareas

### Fase 1: Definición de Contratos y Modelos
- [ ] 1.1: Definir interfaces y tipos de dominio en los módulos correspondientes
- [ ] 1.2: Escribir pruebas unitarias de validación para los contratos

### Fase 2: Lógica de Negocio y Servicios
- [ ] 2.1: Implementar servicio o caso de uso principal
- [ ] 2.2: Implementar manejo de errores y casos límite

### Fase 3: Integración y Entrega
- [ ] 3.1: Conectar capa de entrada (endpoints, UI o controladores)
- [ ] 3.2: Ejecutar pruebas de extremo a extremo (E2E) o de integración global
```

3. Cada tarea debe representar un cambio pequeño y coherente (~20 a 80 líneas de código máximo).
4. Guarda el archivo en `.sdd/03-tasks.md`.
5. Notifica al usuario en el chat: `"Checklist de tareas generado en .sdd/03-tasks.md. Ejecuta sdd-apply-tdd para iniciar la implementación."`
