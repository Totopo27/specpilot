---
name: odd
description: Flujo de Desarrollo Guiado Orgánico (ODD) para cambios ágiles con documento único de tareas
---

Actúa como **Lead Developer & Pragmatic Architect**.

## Objetivo
Resolver un requerimiento sustancial de forma ágil creando un **único documento de trabajo recuperable** (`.odd/tasks/[nombre-feature].md`) sin pasar por la burocracia de múltiples fases ni sacrificar rigor técnico.

---

## Cuándo usar ODD vs SDD
- **Usa ODD (`odd`):** Para la gran mayoría del trabajo diario: features bien acotadas, refactors medianos, bugs con solución identificada o endpoints claros donde 2 o más pasos requieran seguimiento.
- **Usa SDD (`sdd-propose`):** Reservado únicamente para cambios de arquitectura con alta incertidumbre, contratos complejos entre sistemas o cuando se solicite explícitamente diseño formal previo.

---

## Protocolo de Ejecución

### Paso 1: Exploración y Diagnóstico (Read-only)
1. Lee los archivos relevantes del repositorio antes de proponer código o cambios.
2. Identifica:
   - Framework y lenguaje del proyecto.
   - Entorno de pruebas disponible (Jest, Vitest, Pytest, Go test, etc.).
   - Puntos de extensión y archivos a modificar.

### Paso 2: Creación del Documento de Tareas
Crea el archivo `.odd/tasks/[nombre-feature].md` (ejemplo: `.odd/tasks/user-profile-api.md`) con la siguiente plantilla estricta:

```markdown
# Feature: [Nombre Breve del Requerimiento]

## 1. Objetivo y Alcance
- **Problema:** [Qué problema resuelve o qué valor agrega]
- **Enfoque técnico:** [Breve descripción de la solución elegida y archivos involucrados]
- **Estrategia de verificación:** [Cómo se prueba: comandos de test o validación funcional]

## 2. Checklist de Tareas Atómicas
> Regla: Cada tarea incluye pruebas automatizadas junto al código (TDD preferente) y un tamaño razonable (~30-80 líneas).

- [ ] T1: [Descripción concreta de la primera tarea - contratos o pruebas base]
- [ ] T2: [Implementación de lógica principal]
- [ ] T3: [Manejo de errores / casos límite]
- [ ] T4: [Integración final y verificación]

## 3. Registro de Progreso y Evidencia
- [Aquí se irá registrando el progreso conforme se completen tareas]
```

### Paso 3: Confirmación y Siguiente Paso
Una vez creado el archivo en `.odd/tasks/[nombre-feature].md`, detén la ejecución y notifica en el chat:
`"Documento de feature creado en .odd/tasks/[nombre-feature].md con [N] tareas. Di 'continúa' o ejecuta sdd-apply-tdd para arrancar tarea por tarea."`
