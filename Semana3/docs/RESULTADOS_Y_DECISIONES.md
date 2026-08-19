# Resultados y decisiones de la corrida

## Regresión supervisada

| Modelo | MSE test | RMSE test | R² test | Gap R² train-test |
|---|---:|---:|---:|---:|
| Regresión lineal simple | 0.709116 | 0.842090 | 0.458859 | 0.018134 |
| Regresión lineal multivariable | 0.555892 | 0.745581 | 0.575788 | 0.036763 |
| Árbol inicial | 0.524515 | 0.724234 | 0.599732 | 0.037947 |
| MLP regresión | 0.301732 | 0.549301 | 0.769742 | 0.020083 |
| Árbol ajustado | 0.363096 | 0.602575 | 0.722914 | 0.115042 |

El ajuste del árbol evaluó **72 configuraciones** mediante validación cruzada de cinco particiones sobre entrenamiento. La configuración seleccionada fue:

- `max_depth=12`
- `min_samples_leaf=10`
- `min_samples_split=2`

Respecto del árbol inicial, el árbol ajustado redujo MSE en **30.77%**, RMSE en **16.80%** y aumentó R² en **0.123182**.

**Decisión de regresión:** el MLPRegressor se selecciona como modelo predictivo principal porque presenta el menor RMSE y el mayor R² de prueba, además de una brecha train-test menor que la del árbol ajustado.

## Clasificación supervisada

| Arquitectura | Accuracy | Precision | Recall | F1 | Balanced accuracy | Especificidad | FP | FN | Parámetros |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| MLP 1 capa oculta | 0.776536 | 0.754386 | 0.623188 | 0.682540 | 0.747958 | 0.872727 | 14 | 26 | 1001 |
| MLP 2 capas ocultas | 0.793296 | 0.735294 | 0.724638 | 0.729927 | 0.780501 | 0.836364 | 18 | 19 | 6001 |
| MLP 3 capas ocultas | 0.787709 | 0.816327 | 0.579710 | 0.677966 | 0.748946 | 0.918182 | 9 | 29 | 7251 |

**Decisión de clasificación:** el MLP de dos capas ocultas `(100, 50)` se selecciona como la arquitectura más equilibrada de esta corrida porque lidera accuracy, recall, F1 y balanced accuracy y presenta la menor cantidad de falsos negativos. El MLP de tres capas lidera precision y especificidad, pero reduce el recall y exhibe la mayor brecha F1 train-test.

La actividad no define una matriz explícita de costos para falsos positivos y falsos negativos. Por ello la selección prioriza desempeño equilibrado, generalización y complejidad, no una única métrica aislada.
