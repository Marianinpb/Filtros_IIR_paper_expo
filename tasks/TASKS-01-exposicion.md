# Desglose de Tareas: Exposición — Optimal Design of Digital IIR Filters Using Robust Group Search Optimization

> **Plan de referencia:** [plans/PLAN-01-exposicion.md](file:///c:/Users/mtico/Desktop/universidad/Maestria/dsp/Filtros_IIR__paper_expo/plans/PLAN-01-exposicion.md)
> **Fecha:** 2026-05-23
> **Total de tareas:** 7

---

## Leyenda de estado

- `[ ]` — No iniciada
- `[/]` — En progreso
- `[x]` — Completada
- `[!]` — Bloqueada (ver notas al final)

---

## Fase A: Recolección de datos del expositor

- `[x]` **TASK-01:** Solicitar datos del expositor al usuario
  - **_Boundary_:** Interacción completada en fase `/specify`.
  - **_Depends_:** None
  - **Descripción:** Datos recopilados correctamente.

---

## Fase B: Análisis de la fuente y generación de resumen

- `[x]` **TASK-02:** Leer y analizar la fuente de contenido
  - **_Boundary_:** Solo lectura de la fuente. No crea ni modifica archivos.
  - **_Depends_:** TASK-01
  - **Descripción según tipo de fuente:**
    - **paper** (`paper_path` configurado): Leer el PDF `s00034-025-03386-1.pdf`. Extraer título, autores del paper, abstract, conceptos principales y matemática relevante. Enfatizar la rigurosidad matemática.
  - **Criterios de aceptación:**
    - [x] El agente puede describir los 3-5 conceptos principales de la fuente.
    - [x] El agente tiene suficiente información para generar el resumen.
  - **Tests/Verificación:** El agente presenta un listado de conceptos clave al usuario y espera confirmación de que son correctos (o los detalla en el plan).

- `[/]` **TASK-03:** Generar resumen del contenido
  - **_Boundary_:** Solo crea/modifica `resumen_paper.md`.
  - **_Depends_:** TASK-02
  - **Descripción:** Generar un resumen de todo el análisis que incluya contexto, formulación de las optimizaciones, la función de costo que utiliza el algoritmo y por qué R-GSO supera a los otros modelos. Esto servirá de esqueleto para las slides.
  - **Criterios de aceptación:**
    - [x] `resumen_paper.md` ha sido generado en español con los temas estructurados.

---

## Fase C: Generación de la presentación LaTeX

- `[x]` **TASK-04:** Copiar plantilla LaTeX al directorio del proyecto
  - **_Boundary_:** Solo copia archivos de `project_types/exposition/templates/` al directorio `presentacion/` del proyecto. No modifica ningún archivo.
  - **_Depends_:** TASK-01
  - **Descripción:** Inicializa el directorio de LaTeX con las plantillas que provee el SDD Harness.
  - **Criterios de aceptación:**
    - [x] Archivos base (`.tex`, `.sty`, `.bib`, `.png`) disponibles en `presentacion/`.

- `[x]` **TASK-05:** Reemplazar placeholders y generar contenido de diapositivas
  - **_Boundary_:** Solo modifica `presentacion/presentacion.tex`.
  - **_Depends_:** TASK-03, TASK-04
  - **Descripción:** Reemplaza todos los `{{PLACEHOLDERS}}` y genera los frames `\begin{frame}`...`\end{frame}` a partir de `resumen_paper.md`. Insertar ecuaciones formales en código LaTeX para las optimizaciones matemáticas.
  - **Criterios de aceptación:**
    - [x] Todas las instancias de `{{...}}` eliminadas y reemplazadas adecuadamente.

- `[x]` **TASK-06:** Compilar la presentación a PDF
  - **_Boundary_:** Ejecutar terminal para compilación de PDF dentro de `presentacion/`.
  - **_Depends_:** TASK-05
  - **Descripción:** Llama a `pdflatex`. (Si falla, informa / intenta solventar).
  - **Criterios de aceptación:**
    - [x] `presentacion.pdf` compilado.

---

## Fase D: Generación del guion de exposición

- `[x]` **TASK-07:** Generar guion de exposición alineado con las diapositivas
  - **_Boundary_:** Escribir en `guion_exposicion.md`.
  - **_Depends_:** TASK-05
  - **Descripción:** Escribir un guion narrativo, indicando explícitamente cuándo cambiar de diapositiva y qué decir, adaptado a una presentación formal ante un doctor en física exigente.
  - **Criterios de aceptación:**
    - [x] Cada frame de la presentación tiene su contraparte en el guion.

---

## Resumen de progreso

| Fase | Total | Hecha | En progreso | Bloqueada |
|------|-------|-------|-------------|-----------|
| A — Datos del expositor | 1 | 1 | 0 | 0 |
| B — Análisis y resumen | 2 | 2 | 0 | 0 |
| C — Presentación LaTeX | 3 | 3 | 0 | 0 |
| D — Guion | 1 | 1 | 0 | 0 |
| **Total** | **7** | **7** | **0** | **0** |
