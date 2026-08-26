# Semana 4 · Evaluación Sumativa 3 · Fase 4

Estado: **ejecución final archivada y auditada**.

## Propósito

Esta fase evalúa y valida el modelo de clasificación seleccionado al cierre de Semana 3 para el caso Titanic. El trabajo mantiene continuidad con el proyecto ABP, reproduce la partición histórica, documenta el desempeño Hold-Out y estima la estabilidad mediante validación cruzada estratificada aplicada exclusivamente al subconjunto de entrenamiento.

## Contenido

- `data/`: copia verificable del dataset Titanic utilizada por la corrida.
- `notebook/F4_Evaluacion.ipynb`: notebook ejecutado de principio a fin.
- `outputs/`: resultados tabulados, predicciones, controles y manifiesto generados automáticamente.
- `figures/`: ocho visualizaciones derivadas de la misma ejecución.
- `docs/`: decisiones metodológicas, fuentes, guía de ejecución, resultados, trazabilidad y auditoría final.
- `informe/`: informe institucional final en DOCX y PDF.

## Modelo evaluado

- Variable objetivo: `survived`.
- Clase positiva: `1` (`sobrevivió`).
- Predictores de entrada: `pclass`, `age`, `sibsp`, `parch`, `fare`, `sex`, `embarked`.
- Modelo: `MLPClassifier(hidden_layer_sizes=(100, 50))`, seleccionado en Semana 3.
- Umbral de clasificación: `0.50`, conservado por continuidad y no optimizado con test.

## Protocolo de evaluación

- Hold-Out histórico: 80/20 estratificado, `random_state=42`.
- Train: 712 observaciones.
- Test: 179 observaciones.
- Validación de estabilidad: `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)` únicamente sobre train.
- Preprocesamiento: imputación, One-Hot Encoding y estandarización dentro de un único `Pipeline`, reajustado en cada fold.
- Métricas principales: accuracy, precision, recall y F1-score.
- Métricas complementarias: balanced accuracy, especificidad, ROC-AUC y average precision.


## Entorno reproducible

La raíz del repositorio contiene `requirements.txt`, validado contra los imports utilizados en las cuatro semanas. La corrida archivada de Semana 4 registró Python 3.12.4, NumPy 1.26.4, pandas 2.2.2, scikit-learn 1.4.2 y Matplotlib 3.8.4.

Desde la raíz:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

## Resultados principales

### Hold-Out histórico

| Métrica | Valor |
|---|---:|
| Accuracy | 0.793296 |
| Precision | 0.735294 |
| Recall | 0.724638 |
| F1-score | 0.729927 |
| Balanced accuracy | 0.780501 |
| Especificidad | 0.836364 |
| ROC-AUC | 0.852174 |
| Average precision | 0.789082 |

Matriz de confusión:

```text
TN = 92
FP = 18
FN = 19
TP = 50
```

### Validación cruzada estratificada

| Métrica | Promedio | Desv. estándar muestral |
|---|---:|---:|
| Accuracy | 0.825845 | 0.013486 |
| Precision | 0.834689 | 0.041732 |
| Recall | 0.684983 | 0.061566 |
| F1-score | 0.749988 | 0.028931 |
| ROC-AUC | 0.862269 | 0.019814 |

La variabilidad es baja para accuracy y moderada para recall. El recall oscila entre 0.6111 y 0.7593; por ello la estabilidad no se describe de forma uniforme para todas las métricas.

## Consideración metodológica sobre el Hold-Out

La partición Hold-Out de 179 observaciones ya participó en la comparación de arquitecturas de Semana 3. En Semana 4 se conserva como evidencia histórica y de continuidad, no como una muestra completamente independiente posterior a la selección. La evidencia nueva de estabilidad procede del K-Fold estratificado ejecutado solo sobre entrenamiento. No se utilizan observaciones de test para ajustar arquitectura, hiperparámetros, preprocesamiento o umbral.

## Controles de la corrida

- 9/9 celdas de código ejecutadas secuencialmente.
- 0 errores almacenados.
- 0 `ConvergenceWarning` en la corrida archivada.
- 50/50 artefactos requeridos presentes al cierre de la ejecución.
- Continuidad de configuración, métricas y predicciones con Semana 3 verificada.
- Integridad del dataset comprobada mediante SHA-256.
- Última celda:

```text
Control final de consistencia: OK
Continuidad con Semana 3: OK
Artefactos requeridos: OK
```

## Evidencia principal

- [Notebook ejecutado](notebook/F4_Evaluacion.ipynb)
- [Informe final PDF](informe/MCDI504_S4_2_GRUPO6.pdf)
- [Informe final DOCX](informe/MCDI504_S4_2_GRUPO6.docx)
- [Decisiones metodológicas](docs/DECISIONES_METODOLOGICAS.md)
- [Resultados y decisiones](docs/RESULTADOS_Y_DECISIONES.md)
- [Trazabilidad de la rúbrica](docs/TRAZABILIDAD_RUBRICA.md)
- [Auditoría final](docs/AUDITORIA_FINAL.md)
- [Fuentes base](docs/FUENTES_BASE.md)
- [Guía de ejecución](docs/GUIA_EJECUCION.md)
- [Manifiesto final de Semana 4](docs/MANIFIESTO_REPOSITORIO_FINAL.csv)
- [Datos](data/)
- [Outputs](outputs/)
- [Figuras](figures/)
