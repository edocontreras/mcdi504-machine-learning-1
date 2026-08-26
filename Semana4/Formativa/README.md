# Semana 4 · Evaluación Formativa 4 · Avance de la Fase 4

Estado: **ejecución final archivada y validada**.

## Propósito

Esta carpeta documenta la Evaluación Formativa 4 del proyecto ABP de MCDI504. El avance evalúa siete modelos de clasificación sobre Titanic y aplica validación cruzada estratificada de cinco folds al MLP con una capa oculta, tal como exige la pauta formativa.

## Estructura

- `notebook/F4_Evaluacion.ipynb`: notebook ejecutado de principio a fin.
- `outputs/`: tablas, predicciones, métricas, controles y manifiesto de la ejecución.
- `figures/`: 18 figuras generadas por el notebook.
- `docs/`: decisiones metodológicas, resultados, fuentes, trazabilidad, guía y auditoría.
- `data/`: documentación del origen del dataset; la copia canónica se reutiliza desde `Semana3/data/titanic.csv`.
- `informe/`: informe institucional en DOCX y PDF.

## Protocolo

- Dataset: Titanic, 891 observaciones.
- Variable objetivo: `survived`.
- Clase positiva: `1 = sobrevivió`.
- Hold-Out: 80/20 estratificado, `random_state=42` (712 train, 179 test).
- Modelos: KNN, árbol de decisión, SVM RBF, Gaussian Naive Bayes y MLP de 1, 2 y 3 capas ocultas.
- Validación exigida: `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)` sobre train para el MLP de una capa oculta.
- Preprocesamiento: imputación, codificación y escalamiento dentro de `Pipeline`/`ColumnTransformer`, reajustado dentro de cada fold.

## Resultados principales

En Hold-Out, SVM obtuvo la mayor accuracy (0.8324) y el mayor F1-score (0.7656). El MLP de dos capas obtuvo el mayor ROC-AUC (0.8522) y el mayor recall entre los siete modelos (0.7246). El MLP de una capa, requerido para validación cruzada, alcanzó accuracy media de 0.8076 ± 0.0167 y F1 media de 0.7277 ± 0.0161 en cinco folds.

La matriz OOF agregada del MLP de una capa fue `[[392, 47], [90, 183]]`; por ello la detección de la clase positiva sigue siendo el principal aspecto a mejorar.

## Reproducción

Desde la raíz del repositorio:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

Abrir `Semana4/Formativa/notebook/F4_Evaluacion.ipynb` y ejecutar todas las celdas en orden.

## Evidencia

- [Notebook](notebook/F4_Evaluacion.ipynb)
- [Informe PDF](informe/MCDI504_S4_1_GRUPO6.pdf)
- [Informe DOCX](informe/MCDI504_S4_1_GRUPO6.docx)
- [Trazabilidad de rúbrica](docs/TRAZABILIDAD_RUBRICA.md)
- [Auditoría final](docs/AUDITORIA_FINAL.md)
- [Resultados y decisiones](docs/RESULTADOS_Y_DECISIONES.md)
- [Decisiones metodológicas](docs/DECISIONES_METODOLOGICAS.md)
- [Fuentes base](docs/FUENTES_BASE.md)
- [Guía de ejecución](docs/GUIA_EJECUCION.md)

Repositorio público: https://github.com/edocontreras/mcdi504-machine-learning-1
