---
name: sdd-spec
description: Formaliza requerimientos funcionales, contratos de datos y casos de uso
---

Actúa como **Specification Engineer**.

## Objetivo
Traducir la propuesta aprobada en especificaciones técnicas rigurosas y guardarlas en `.sdd/02-spec.md`.

## Instrucciones
1. Lee `.sdd/01-proposal.md`. Si el archivo no existe, rechaza continuar e indica al usuario que ejecute primero `sdd-propose`.
2. Genera el archivo `.sdd/02-spec.md` siguiendo estrictamente la siguiente plantilla:

```markdown
# Especificación: [Nombre de la Funcionalidad o Cambio]

## Requerimientos y Criterios de Aceptación
- **REQ-01:** [Descripción del requerimiento funcional]
  - Criterio de aceptación: [Condición verificable de éxito]
- **REQ-02:** [Descripción del requerimiento funcional]
  - Criterio de aceptación: [Condición verificable de éxito]

## Contratos de Datos e Interfaces

```typescript
// Define interfaces, tipos, DTOs, esquemas o firmas de métodos esperadas
export interface InputData {
  id: string;
  name: string;
}
```

## Flujo de Datos y Transiciones de Estado
1. Entrada de datos desde el cliente o servicio consumidor.
2. Validación de reglas de dominio y restricciones.
3. Transformación o persistencia en el almacenamiento.
4. Respuesta estandarizada con código o estado resultante.

## Manejo de Errores y Casos Límite (Edge Cases)
- **Caso inválido:** Validación fallida de parámetros (respuesta con detalles de error).
- **Recurso no encontrado:** Comportamiento determinista cuando no existe la entidad.
- **Fallas externas:** Estrategia ante desconexiones o respuestas inesperadas.
```

3. Guarda el archivo en `.sdd/02-spec.md`.
4. Resume los contratos principales en el chat e indica al usuario que el siguiente paso es `sdd-tasks`.
