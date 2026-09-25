# EduCurator AI — Proyecto de investigación V1 (LaTeX)

Versión nueva del proyecto, construida sobre el ajuste de enfoque
(`EduCurator_estructura_investigacion_en_curso.md`) y con las 38 fuentes reales
leídas en `Claude outputs/fichas-extraccion-EduCurator.md`.

## Cómo compilar

**Overleaf (recomendado).** Subir la carpeta completa, abrir `main.tex`,
y en *Menu → Settings* dejar compilador **pdfLaTeX** (Overleaf ejecuta biber
automáticamente al detectar `biblatex`).

**Local** (requiere TeX Live o MiKTeX con `biblatex`, `biber`, `tcolorbox`,
`titlesec`, `cleveref`, `csquotes`):

```bash
latexmk -pdf -bibtex-cond main.tex
```

o, paso a paso:

```bash
pdflatex main && biber main && pdflatex main && pdflatex main
```

> En este equipo no hay una instalación de LaTeX, así que el documento **no se ha
> compilado todavía**. La sintaxis se revisó manualmente (balance de llaves y
> entornos, y verificación cruzada de que toda clave citada existe en
> `referencias.bib`), pero la primera compilación real debe hacerse en Overleaf.

## Estructura de archivos

```
V1-LaTeX/
├── main.tex              Documento maestro; controla qué partes se incluyen
├── preambulo.tex         Paquetes, estilos, cajas y comandos propios
├── referencias.bib       38 fuentes núcleo, APA 7 con DOI
└── secciones/
    ├── 00-portada.tex
    ├── 01-resumen.tex                   Resumen + Abstract
    ├── 02-introduccion.tex              §1
    ├── 03-contexto-del-problema.tex     §2
    ├── 04-problema-de-investigacion.tex §3
    ├── 05-justificacion.tex             §4
    ├── 06-antecedentes.tex              §5
    ├── 07-estado-del-arte.tex           §6
    ├── 08-marco-teorico.tex             §7
    ├── 09-marco-conceptual.tex          §8
    └── 10-brecha-de-investigacion.tex   §9
```

Las partes aún no escritas están como `\input` comentados en `main.tex`, con el
nombre de archivo ya previsto. Para activarlas basta descomentar la línea.

## Plan de bloques

| Bloque | Contenido | Estado |
|---|---|---|
| 0 | Andamiaje LaTeX + `referencias.bib` (38 fuentes) | **Listo** |
| 1 | Parte I — Contexto y problema | **Listo** |
| 2 | Parte II — Antecedentes, estado del arte, marco teórico, marco conceptual, brecha | **Listo** |
| 3 | Parte III — Preguntas, objetivos, proposiciones, variables, modelo conceptual (TikZ) | Pendiente |
| 4 | Parte IV — Artefacto: descripción, arquitectura, componentes de IA, benchmark, estado del MVP | Pendiente |
| 5 | Parte V — Metodología de evaluación: DSR, diseño experimental, ground truth, baselines, ablaciones, instrumentos, métricas, plan de análisis, reproducibilidad | Pendiente |
| 6 | Parte VI — Estado de avance, evidencia disponible, pendientes, riesgos | Pendiente |
| 7 | Parte VII — Resultados esperados, contribuciones, cronograma, ética, anexos | Pendiente |

## Convenciones del documento

### Cajas semánticas

- `\begin{advertencia}...\end{advertencia}` — delimita lo que **no** se puede
  afirmar citando una fuente. Nace del campo "Qué NO demuestra" de las fichas.
- `\begin{estado}...\end{estado}` — enmarca una declaración de alcance, una
  consecuencia de diseño o una lectura conjunta de varias fuentes.

### Marcadores de pendiente

`\pend{texto}` imprime un marcador rojo visible. Se desactivan todos de golpe
cambiando `\pendienteactivotrue` por `\pendienteactivofalse` en `preambulo.tex`
antes de la entrega.

### Criterio de clasificación de enunciados

Cada afirmación sustantiva es (A) lo que la literatura demuestra, (B) lo que el
MVP implementa, (C) lo que la investigación propone evaluar o (D) lo que se
desconoce. Está explicado en §1.4 del documento y es el criterio de revisión de
cada sección nueva.

## Decisiones tomadas en el Bloque 0–1

1. **Título.** Se adoptó la opción A del documento de ajuste de enfoque:
   *"EduCurator AI: desarrollo y evaluación en curso de un sistema agéntico para la
   curación asistida de contenidos educativos"*.
2. **Fuente [23] corregida.** La matriz registraba Holmes, Bialik & Fadel (2019),
   pero el PDF disponible es Miao, Holmes, Huang & Zhang (2021), *AI and education:
   Guidance for policy-makers* (UNESCO). En el `.bib` está la fuente real. **La
   matriz bibliográfica debe corregirse.**
3. **NIST AI RMF** se cita con autor institucional (`National Institute of Standards
   and Technology`), no como "Tabassi (2023)", para mantener una sola forma.
4. **Referencias eliminadas del V0.** Ji et al. (2023) sobre alucinación y Vaswani
   et al. (2017) sobre Transformers no están en el núcleo de 38 fuentes. La primera
   se reemplazó por Huang et al. (2025), que sí se leyó. Si el marco teórico de la
   Parte II necesita citar la arquitectura Transformer, hay que añadir la fuente al
   núcleo y leerla.
5. **Ninguna afirmación de eficacia.** Se eliminaron del V0 los enunciados que
   presentaban beneficios como establecidos. La sección de justificación práctica se
   reformuló como una apuesta falsable, no como un beneficio esperado.
6. **Atchley et al. [21]** — la ficha recomienda bajarlo de Núcleo a Apoyo (es un
   ensayo de perspectiva sin datos). Aún no se ha citado; se usará como contexto en
   la Parte II, no como evidencia.

## Decisiones tomadas en el Bloque 2

1. **División de trabajo entre secciones.** Antecedentes = trayectoria histórica y
   dónde se detuvo cada línea. Estado del arte = qué está establecido hoy, con cifras,
   por las ocho líneas de la matriz. Marco teórico = los constructos y su papel en el
   diseño de la investigación, no descripción de tecnologías (eso va en la Parte IV).
   Marco conceptual = definiciones operacionales y distinciones que el documento
   mantiene.
2. **Líneas A y B no se repiten.** Su contenido sustantivo está en §2 (contexto del
   problema); §6.1 solo retoma los tres resultados que condicionan el diseño y
   remite. Evita duplicar media Parte I.
3. **Tabla de distinciones (§8.4).** Ocho pares de términos que no deben usarse como
   equivalentes (similitud ≠ confianza ≠ calibración, contradicción ≠ sin evidencia,
   trazabilidad del proceso ≠ fundamentación de la salida, etc.). Es la defensa contra
   el error más probable en la exposición oral.
4. **La brecha se formuló estrecha a propósito.** No se afirma que falte investigación
   sobre IA en educación ni sobre RAG. Se afirma que la intersección específica
   —inconsistencia intracorpus como *objeto*, corpus de curso, español, atribución por
   componentes— no está cubierta. El argumento central: Lewis et al. (2020) declaran
   explícitamente que no abordan qué ocurre cuando la fuente se contradice
   internamente, que es justamente el caso de este proyecto.
5. **Controles negativos como requisito.** Gubelmann et al. (2024) muestran que con
   desbalance realista un modelo puede colapsar atribuyendo relaciones inexistentes.
   Un benchmark solo con defectos plantados mide *recall* y no dice nada sobre
   precisión. Queda fijado en §8.2 y condiciona el Bloque 4.
6. **Atchley et al. [21] y Miao et al. [23]** se usan con advertencia explícita de que
   son ensayo de perspectiva y documento de política, sin evidencia empírica propia.
7. **`xltabular` en lugar de `longtable`.** Las columnas `X` no funcionan dentro de
   `longtable`; las tablas largas de las Partes II y V usan `xltabular`.

## Pendientes que arrastra el Bloque 1

- Verificar los datos editoriales marcados `[VERIFICAR]` en `referencias.bib`
  (preprints y manuscritos aceptados: Clements, Xie, Koreeda, Zhan, Thakur,
  Mohammadi, Ru, Mehrotra, Lewis, Hevner).
- Confirmar el nombre exacto de la facultad y el programa en la portada.
- Decidir si el documento lleva Abstract en inglés en la versión final.
