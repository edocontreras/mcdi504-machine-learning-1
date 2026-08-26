# Resultados y decisiones · Formativa 4

## Hold-Out

- Mejor accuracy: **SVM = 0.8324**.
- Mejor F1-score: **SVM = 0.7656**.
- Mejor recall: **MLP 2 capas = 0.7246**.
- Mejor ROC-AUC: **MLP 2 capas = 0.8522**.
- MLP 1 capa (modelo exigido para CV): accuracy 0.7765, precision 0.7544, recall 0.6232 y F1 0.6825.

La lectura preliminar favorece SVM por balance accuracy/F1 y baja cantidad de FP (10) y FN (20). Sin embargo, esta comparación procede de una única partición Hold-Out; no equivale a una validación cruzada comparativa de todos los candidatos.

## Validación cruzada del MLP de una capa

- Accuracy media: **0.8076 ± 0.0167**.
- Precision media: **0.8021 ± 0.0630**.
- Recall media: **0.6704 ± 0.0426**.
- F1 media: **0.7277 ± 0.0161**.
- ROC-AUC media: **0.8571 ± 0.0183**.
- Matriz OOF agregada: **[[392, 47], [90, 183]]**.

Accuracy y F1 presentan baja variabilidad entre folds. Precision, recall y especificidad son más sensibles a la composición de cada fold. La principal limitación es el número de falsos negativos de la clase positiva, coherente con recall OOF de 0.6703.

## Implicación preliminar

Para el avance formativo, SVM es el candidato con mejor desempeño puntual en Hold-Out, mientras que el MLP de una capa aporta la evidencia de estabilidad exigida por la actividad. Una selección final entre familias debería aplicar un protocolo de validación comparable a todos los candidatos y considerar el costo relativo de FP y FN.
