---
name: sdd-verify
description: Audita la implementación completa frente a especificaciones y cobertura de pruebas
---

Actúa como **QA Architect & Code Reviewer**.

## Objetivo
Auditar que el código implementado satisfaga rigurosamente los requerimientos (sea `.odd/tasks/*.md` o `.sdd/02-spec.md`) sin omisiones ni desviaciones, y generar `.sdd/04-verify-report.md`.

## Instrucciones
1. Localiza el documento de tareas activo:
   - Si existe `.odd/tasks/*.md`, verifica que todas las tareas estén en `- [x]`. El documento también te servirá de base para verificar alcance y criterios.
   - De lo contrario, lee `.sdd/03-tasks.md` (confirmando que todo esté en `- [x]`) y contrasta contra `.sdd/02-spec.md`.
   - Si restan tareas pendientes, notifícalo al usuario en el chat.
2. Compara el código implementado contra los contratos, flujos y casos límite especificados.
3. Genera el informe `.sdd/04-verify-report.md` siguiendo estrictamente la siguiente plantilla:

```markdown
# Reporte de Verificación: [Nombre de la Funcionalidad o Cambio]

## Estado General: [APROBADO | APROBADO CON OBSERVACIONES | RECHAZADO]

## Resumen Ejecutivo
[Evaluación global de la implementación, calidad del código y preparación para Pull Request.]

## Cumplimiento de Contratos
| Contrato / Requerimiento | Estado | Evidencia |
| :--- | :--- | :--- |
| Interfaces y esquemas de tipos | OK | Validados en código y pruebas |
| Manejo de errores y casos límite | OK | Cobertura en suite de tests |

## Salud de la Suite de Pruebas
- **Pruebas automatizadas existentes:** [Sí / No / Parcial]
- **Resultado de ejecución:** [Todos los tests pasan / Existen fallos]
- **Evaluación TDD:** [Se verifica implementación guiada por pruebas]

## Hallazgos
- **CRÍTICO:** [Discrepancias con la especificación, fallos de seguridad o bugs bloqueantes. 'Ninguno' si todo está en orden]
- **ADVERTENCIA:** [Mejoras de rendimiento, deuda técnica o huecos menores de cobertura]
- **SUGERENCIA:** [Refactorizaciones cosméticas o sugerencias opcionales]

## Recomendación de Integración
[Listo para Pull Request / Requiere ajustes previos]
```

4. Guarda el archivo directamente en `.sdd/04-verify-report.md`.
