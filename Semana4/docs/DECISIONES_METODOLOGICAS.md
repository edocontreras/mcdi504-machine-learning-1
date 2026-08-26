# Decisiones metodológicas y analíticas

## Continuidad del proyecto

- Dataset: Titanic.
- Fuente: `Semana3/data/titanic.csv`, copiada y verificada en `Semana4/data/titanic.csv`.
- Objetivo binario: `survived`.
- Clase positiva: `1` (`sobrevivió`).
- Modelo validado: MLP de dos capas ocultas `(100, 50)`, seleccionado en Semana 3.
- No se realiza una nueva selección de arquitectura en Semana 4.

## Predictores y preprocesamiento

- Predictores: `pclass`, `age`, `sibsp`, `parch`, `fare`, `sex`, `embarked`.
- `alive` permanece excluida por fuga directa respecto de `survived`.
- El preprocesamiento se integra en `Pipeline`: imputación, codificación One-Hot, escalamiento y MLP.
- En validación cruzada, el `Pipeline` se reajusta en cada fold para impedir que parámetros aprendidos incorporen información del fold de validación.

## Partición y validación

- Hold-Out histórico: 80/20 estratificado, `random_state=42`, 712 train y 179 test.
- La partición Hold-Out ya participó en la comparación de arquitecturas de Semana 3; se declara explícitamente como limitación y evidencia histórica, no como test virgen posterior a la selección.
- Estabilidad: `StratifiedKFold(k=5, shuffle=True, random_state=42)` aplicado únicamente a train.
- K-Fold se selecciona como compromiso entre uso de los datos, estabilidad y costo. En esta corrida requiere 5 ajustes externos frente a 1 de Hold-Out y 712 ajustes teóricos de LOOCV.

## Métricas

- Principales: accuracy, precision, recall y F1-score.
- Complementarias: balanced accuracy, especificidad, ROC-AUC y average precision.
- Umbral: 0.50, consistente con `MLPClassifier.predict`; no se optimiza con test debido a que el caso no define una función de costos.

## Criterio de lectura

La evaluación no se reduce a una métrica aislada. Se consideran errores FP/FN, discriminación, estabilidad entre folds, costo del protocolo y limitaciones de generalización. En particular, el recall presenta mayor variabilidad que accuracy, por lo que no se describe la estabilidad como homogénea para todas las métricas.
