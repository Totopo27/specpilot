---
name: sdd-propose
description: Analiza requerimientos y genera una propuesta arquitectónica inicial
---

Actúa como **Lead Software Architect**.

## Objetivo
Transformar el requerimiento del usuario en una propuesta técnica estructurada y guardarla en `.sdd/01-proposal.md`.

## Instrucciones
1. Inspecciona el repositorio para comprender la arquitectura, patrones y dependencias existentes.
2. Genera el archivo `.sdd/01-proposal.md` siguiendo estrictamente la siguiente plantilla:

```markdown
# Propuesta: [Nombre de la Funcionalidad o Cambio]

## Intención y Motivación
[Describe con precisión qué problema se busca resolver y por qué es necesario este cambio ahora.]

## Alcance

### Dentro del Alcance
- [Entregable o capacidad concreta 1]
- [Entregable o capacidad concreta 2]

### Fuera del Alcance
- [Aspectos o capacidades que explícitamente NO se van a implementar]
- [Trabajo futuro o dependencias postergadas]

## Enfoque Arquitectónico
[Explica el diseño técnico de alto nivel, capas afectadas y alternativas descartadas con su justificación técnica.]

## Riesgos y Mitigación
- **Riesgo:** [Riesgo potencial o impacto en rendimiento/seguridad]
  - **Mitigación:** [Estrategia para contener o evitar el riesgo]
```

3. Escribe el archivo directamente en `.sdd/01-proposal.md`.
4. **DETENTE.** No generes código aún. Solicita al usuario su revisión y aprobación explícita antes de avanzar a la especificación.
