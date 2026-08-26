# Decisiones metodológicas · Formativa 4

1. **Partición Hold-Out estratificada 80/20.** Se conserva `random_state=42` y `stratify=y`, coherente con la fase de clasificación de Semana 3 y con la proporción 61.6/38.4 de la variable objetivo.
2. **Clase positiva.** `survived=1` se utiliza como evento positivo para precision, recall y F1-score.
3. **Preprocesamiento dentro del pipeline.** Imputación, codificación y escalamiento se ajustan con datos de entrenamiento. En validación cruzada, cada fold reajusta el pipeline completo para evitar filtración de información.
4. **Escalamiento por modelo.** KNN, SVM y MLP incluyen estandarización numérica; árbol de decisión y GaussianNB no requieren el mismo tratamiento geométrico.
5. **Validación del MLP de una capa.** Se utiliza `StratifiedKFold(k=5)` por tratarse de clasificación binaria con clases desiguales. Esta variante conserva la lógica K-Fold y reduce variaciones de prevalencia entre folds.
6. **No selección por una sola métrica.** La comparación utiliza accuracy, precision, recall, F1, matriz de confusión y métricas complementarias ROC-AUC/AP. El ranking por F1 es evidencia preliminar, no una selección definitiva sin validación equivalente de todos los modelos.
7. **Costo de validación.** K-Fold requiere 5 ajustes del MLP de una capa frente a 1 en Hold-Out y 712 en Leave-One-Out para este train; se utiliza como compromiso entre costo y estabilidad.
8. **Continuidad.** Las arquitecturas y métricas Hold-Out de los tres MLP coinciden exactamente con Semana 3, según `15_continuidad_mlp_semana3.csv`.
