# Decisiones técnicas - Semana 2

## Variable objetivo
`MedHouseVal` se utiliza como variable continua a predecir.

## Partición
Se aplica una partición 80% entrenamiento y 20% prueba con `random_state=42`.

## Valores faltantes
El notebook verifica los valores faltantes antes del modelamiento. La carga estándar de California Housing no requiere imputación.

## Regresión lineal simple
El predictor se selecciona mediante correlación de Pearson calculada únicamente en entrenamiento. El predictor seleccionado se estandariza con los parámetros aprendidos desde `X_train`.

## Estandarización
`StandardScaler` se ajusta exclusivamente con `X_train` y transforma posteriormente entrenamiento y prueba.

## Árbol de decisión
Se utiliza `DecisionTreeRegressor` con `max_depth=5` y `random_state=42`, junto con los parámetros básicos registrados en la ficha técnica.

## Red neuronal
Se utiliza `MLPRegressor` con una capa oculta de 100 neuronas, ReLU, Adam, `max_iter=500`, `early_stopping=True` y `random_state=42`.

## Evaluación
MSE, RMSE y R² se calculan sobre el mismo conjunto de prueba.

## Análisis complementario
Se conserva una regresión lineal multivariable con las ocho variables estandarizadas para disponer de una comparación adicional con árbol y MLP usando el mismo conjunto de predictores.
