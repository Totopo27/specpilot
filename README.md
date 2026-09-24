# SpecPilot

Framework de Desarrollo Guiado por Especificaciones (SDD) y Desarrollo Guiado Orgánico (ODD) para GitHub Copilot.
Arquitectura basada en máquina de estados sobre el sistema de archivos, sin instalaciones externas.

---

## Contexto

GitHub Copilot opera bajo una interfaz de modelo de lenguaje de hilo único (single-threaded). Conforme la conversación avanza, presenta problemas frecuentes:
1. Degradación de contexto y pérdida de memoria: Olvida decisiones arquitectónicas y restricciones previas.
2. Generación prematura de código: Escribe implementaciones antes de definir contratos, límites y casos de prueba.
3. Sobrecarga de burocracia: Aplicar un pipeline completo de especificaciones para cambios pequeños agota tokens y desgasta el flujo de trabajo.

SpecPilot traslada el patrón de máquina de estados guiada por artefactos (utilizado por Gentle AI) directamente a GitHub Copilot, ofreciendo dos carriles complementarios:
- **ODD (Organic Driven Development - Recomendado para el día a día):** Un único documento ágil y recuperable (`.odd/tasks/<feature>.md`) que desglosa el objetivo, alcance y tareas atómicas para entrar directo a implementar con TDD.
- **SDD (Spec-Driven Development - Para arquitectura compleja):** Pipeline formal de 4 fases (`01-proposal` ➔ `02-spec` ➔ `03-tasks` ➔ `04-verify`) para cuando hay alta incertidumbre o necesidad de contratos blindados.

---

## Principios Fundamentales

1. El sistema de archivos es la memoria: El historial de chat es volátil; los archivos en disco son deterministas. Cada fase o tarea persiste su entregable íntegro en disco antes de concluir.
2. Amnesia controlada: Al iniciar o retomar una tarea, Copilot debe leer de forma obligatoria el archivo de tareas activo (`.odd/tasks/*.md` o `.sdd/03-tasks.md`) en lugar de confiar en el contexto acumulado del chat.
3. El trabajo chico se mantiene chico: No abras 4 documentos para un cambio acotado. Usa ODD para planificar e implementar en un solo ciclo.
4. Desarrollo guiado por pruebas por defecto (Strict TDD): La implementación aplica por defecto el ciclo Red-Green-Refactor (`sdd-apply-tdd`). Se mantiene disponible un modo rápido directo (`sdd-apply`) para casos puntuales.
5. Unidades de trabajo atómicas: La ejecución avanza tarea por tarea, marcando los elementos completados (`[x]`) de manera incremental con evidencia.
6. Prompts autocontenidos: Cada archivo de fase incluye sus propias reglas y la plantilla exacta del documento a generar.

---

## Estructura del Repositorio

```text
.
├── .github/
│   ├── copilot-instructions.md          # Reglas maestras de comportamiento para Copilot
│   └── prompts/                         # Prompts modulares autocontenidos
│       ├── odd.prompt.md                # Flujo Orgánico ágil (un solo documento de tareas)
│       ├── sdd-propose.prompt.md        # Propuesta técnica formal y alcance (SDD)
│       ├── sdd-spec.prompt.md           # Requisitos y contratos de datos (SDD)
│       ├── sdd-tasks.prompt.md          # Desglose de tareas atómicas (SDD)
│       ├── sdd-apply-tdd.prompt.md      # Implementación con TDD estricto (por defecto para ODD y SDD)
│       ├── sdd-apply.prompt.md          # Implementación directa / modo rápido
│       └── sdd-verify.prompt.md         # Auditoría de código y reporte de verificación
├── .odd/                                # Estado activo de features bajo flujo ODD
│   └── tasks/
│       └── .gitkeep
├── .sdd/                                # Estado activo de features bajo flujo formal SDD
│   └── .gitkeep
└── README.md
```

---

## Ciclos de Vida

### 🌿 Carril ODD (Orgánico / Recomendado para el día a día)
```text
Requerimiento del Usuario
          │
          ▼
       [ odd ]       ──► Genera `.odd/tasks/<feature>.md` (Alcance + Checklist)
          │
          ▼
   [ sdd-apply-tdd ] ──► Escribe Test (RED) ──► Código Mínimo (GREEN) ──► Refactor ──► Marca `[x]`
    (o sdd-apply)
          │
          ▼ (Al completar el checklist)
   [ sdd-verify ]    ──► Genera `.sdd/04-verify-report.md` ──► Listo para PR
```

### 🏛️ Carril SDD (Formal / Para alta incertidumbre arquitectónica)
```text
Requerimiento de Alta Complejidad
          │
          ▼
   [ sdd-propose ]   ──► Genera `.sdd/01-proposal.md`
          │
          ▼ (Aprobación del usuario)
   [ sdd-spec ]      ──► Genera `.sdd/02-spec.md`
          │
          ▼
   [ sdd-tasks ]     ──► Genera `.sdd/03-tasks.md`
          │
          ▼
   [ sdd-apply-tdd ] ──► Ciclo Red-Green-Refactor por tarea
          │
          ▼
   [ sdd-verify ]    ──► Genera `.sdd/04-verify-report.md`
```

---

## Guía de Uso

### Opción A: Flujo Orgánico ODD (Recomendado)
1. **Planificar la feature en Copilot Chat:**
   ```text
   Usa odd para: [descripción de la funcionalidad o refactor]
   ```
   Copilot explorará el código y creará `.odd/tasks/<nombre-feature>.md` con el checklist inicial.
2. **Implementar tarea por tarea con TDD:**
   ```text
   Ejecuta sdd-apply-tdd
   ```
3. **Verificar y cerrar:**
   ```text
   Ejecuta sdd-verify
   ```

### Opción B: Flujo Formal SDD
1. **Iniciar propuesta:** `Usa sdd-propose para diseñar: [requerimiento]`
2. **Especificar contratos:** `Ejecuta sdd-spec`
3. **Desglosar tareas:** `Ejecuta sdd-tasks`
4. **Implementar con TDD:** `Ejecuta sdd-apply-tdd`
5. **Auditar:** `Ejecuta sdd-verify`
