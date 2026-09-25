# SpecPilot

Framework de Desarrollo Guiado por Especificaciones (SDD) y Desarrollo Guiado Orgánico (ODD) para GitHub Copilot.
Arquitectura basada en máquina de estados sobre el sistema de archivos, sin dependencias ni extensiones externas.

---

## Quick Path (Cheat Sheet)

Los 3 pasos esenciales para el 90% del trabajo diario:

1. **Iniciar feature:** `odd: [nombre o descripción de la feature]`  
   Crea el documento único de alcance y tareas en `.odd/tasks/<feature>.md`.
2. **Implementar con TDD:** `sdd-apply-tdd`  
   Avanza tarea por tarea en ciclo Red-Green-Refactor y marca cada elemento completado (`[x]`).
3. **Verificar y Archivar:** `sdd-verify`  
   Audita contratos, suite de pruebas y seguridad (`.sdd/04-verify-report.md`) y archiva la feature a `.odd/archive/`.

---

## Comparativa: ODD vs SDD

| Criterio | ODD (`odd`) — ~90% del trabajo diario | SDD (`sdd-propose`) — Arquitectura formal |
| :--- | :--- | :--- |
| **Enfoque** | Pragmático, directo y ágil | Riguroso, defensivo y multicapa |
| **Cuándo usar** | Features definidas, refactors medianos, endpoints y bugs con solución clara | Arquitectura con alta incertidumbre, contratos críticos entre sistemas o diseño formal previo |
| **Artefactos** | **1 único archivo:** `.odd/tasks/<feature>.md` | **4 fases secuenciales:** `01-proposal` ➔ `02-spec` ➔ `03-tasks` ➔ `04-verify` |
| **Overhead** | Mínimo: arranca inmediatamente con checklist atómico | Moderado: requiere validación explícita de propuesta y contratos antes de codificar |
| **Implementación** | TDD estricto por defecto (`sdd-apply-tdd`) | TDD estricto por defecto (`sdd-apply-tdd`) |
| **Cierre de ciclo** | Auditoría y archivo en `.odd/archive/` | Auditoría y archivo en `.sdd/archive/` |

---

## Contexto y Motivación

GitHub Copilot opera bajo un modelo de lenguaje de hilo conversacional único (single-threaded). Conforme la interacción avanza, surgen tres problemas comunes:
1. **Degradación de contexto y pérdida de memoria:** Se olvidan decisiones arquitectónicas, restricciones previas y contratos acordados.
2. **Generación prematura de código:** Se producen implementaciones apresuradas antes de definir interfaces, límites y casos de prueba.
3. **Sobrecarga burocrática:** Aplicar un pipeline completo de especificaciones formales para tareas cotidianas agota tokens y desacelera el flujo.

SpecPilot traslada el patrón de **máquina de estados guiada por artefactos** directamente al sistema de archivos del repositorio, garantizando persistencia y rigor con mínima fricción.

---

## Principios Fundamentales

1. **El sistema de archivos es la memoria:** El historial de chat es volátil; el disco es determinista. Toda fase o tarea persiste su entregable completo antes de terminar.
2. **Amnesia controlada y desambiguación:** Al iniciar o retomar una tarea, Copilot lee obligatoriamente el archivo activo (`.odd/tasks/*.md` o `.sdd/03-tasks.md`). Si existen múltiples tareas, solicita confirmación explícita.
3. **El trabajo chico se mantiene chico:** No abras pipelines de 4 documentos para cambios cotidianos. Usa ODD para resolver en un solo ciclo ágil.
4. **Desarrollo guiado por pruebas por defecto (Strict TDD):** La implementación ejecuta el ciclo Red-Green-Refactor (`sdd-apply-tdd`). El modo directo (`sdd-apply`) se reserva para configuraciones puras o solicitudes explícitas.
5. **Unidades de trabajo atómicas:** El avance ocurre tarea por tarea, marcando de forma incremental cada checklist (`[x]`) con su respectiva evidencia.
6. **Prompts autocontenidos y seguros:** Cada rol define sus límites de comportamiento, integridad anti-jailbreak y prohibición de exfiltración de datos.

---

## Estructura del Repositorio

```text
.
├── .github/
│   ├── copilot-instructions.md          # Reglas maestras de comportamiento, seguridad y gobernanza
│   └── prompts/                         # Prompts modulares autocontenidos por rol
│       ├── odd.prompt.md                # Flujo Orgánico ágil (documento único de tareas)
│       ├── sdd-propose.prompt.md        # Propuesta técnica y alcance formal (SDD)
│       ├── sdd-spec.prompt.md           # Requisitos y contratos de datos (SDD)
│       ├── sdd-tasks.prompt.md          # Desglose de tareas atómicas (SDD)
│       ├── sdd-apply-tdd.prompt.md      # Implementación con TDD estricto (por defecto)
│       ├── sdd-apply.prompt.md          # Implementación directa / modo rápido
│       └── sdd-verify.prompt.md         # Auditoría, checklist de seguridad y reporte
├── .odd/                                # Estado de features bajo flujo ODD
│   ├── tasks/                           # Feature activa (.odd/tasks/<feature>.md)
│   └── archive/                         # Histórico de features completadas
├── .sdd/                                # Estado de features bajo flujo SDD
│   ├── archive/                         # Histórico de especificaciones completadas
│   └── 04-verify-report.md              # Último reporte de auditoría generado
├── .gitignore                           # Exclusiones de secretos, entornos y artefactos locales
└── README.md
```

---

## Ciclos de Vida

### Carril ODD (Orgánico — Flujo Predeterminado)
```text
Requerimiento
     │
     ▼
  [ odd ]            ──► Crea `.odd/tasks/<feature>.md` (Alcance + Checklist atómico)
     │
     ▼
[ sdd-apply-tdd ]    ──► Test (RED) ──► Código (GREEN) ──► Refactor ──► Marca `[x]`
(o sdd-apply)
     │
     ▼ (Checklist completado)
 [ sdd-verify ]      ──► Genera `.sdd/04-verify-report.md` (Contratos + Tests + Seguridad)
     │
     ▼ (Aprobado)
Archivado & PR       ──► Mueve a `.odd/archive/<feature>.md` ──► Listo para PR
```

### Carril SDD (Formal — Alta Complejidad Arquitectónica)
```text
Requerimiento Complejo
     │
     ▼
 [ sdd-propose ]     ──► Genera `.sdd/01-proposal.md`
     │
     ▼ (Validación de arquitectura)
   [ sdd-spec ]      ──► Genera `.sdd/02-spec.md` (Contratos e interfaces)
     │
     ▼
  [ sdd-tasks ]      ──► Genera `.sdd/03-tasks.md` (Desglose secuencial)
     │
     ▼
[ sdd-apply-tdd ]    ──► Ciclo Red-Green-Refactor por tarea
     │
     ▼
 [ sdd-verify ]      ──► Genera `.sdd/04-verify-report.md`
     │
     ▼ (Aprobado)
Archivado & PR       ──► Mueve a `.sdd/archive/<feature>/` ──► Listo para PR
```

---

## Guía de Uso Paso a Paso

### Opción A: Flujo Orgánico ODD (Recomendado)
1. **Planificar la feature en Copilot Chat:**
   ```text
   Usa odd para: [descripción de la funcionalidad o refactor]
   ```
   Copilot explorará el código base y generará `.odd/tasks/<nombre-feature>.md` con el checklist inicial.
2. **Implementar tarea por tarea con TDD:**
   ```text
   Ejecuta sdd-apply-tdd
   ```
   Copilot toma la siguiente tarea pendiente, escribe la prueba primero, implementa la solución y marca `- [x]`.
3. **Verificar y auditar:**
   ```text
   Ejecuta sdd-verify
   ```
   Genera `.sdd/04-verify-report.md` validando contratos, salud de tests e higiene de seguridad (sin secretos expuestos y validación de entradas).
4. **Archivar para el Pull Request:**
   Mueve el documento completado a `.odd/archive/` para dejar el espacio activo limpio para el próximo cambio.

### Opción B: Flujo Formal SDD
1. **Iniciar propuesta:** `Usa sdd-propose para diseñar: [requerimiento]`
2. **Especificar contratos:** `Ejecuta sdd-spec`
3. **Desglosar tareas:** `Ejecuta sdd-tasks`
4. **Implementar con TDD:** `Ejecuta sdd-apply-tdd`
5. **Auditar y archivar:** `Ejecuta sdd-verify` y traslada los artefactos a `.sdd/archive/`.
