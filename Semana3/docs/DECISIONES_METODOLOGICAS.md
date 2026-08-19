# Decisiones metodológicas y analíticas

## Regresión

- Dataset: California Housing.
- Objetivo: `MedHouseVal`, variable continua.
- Split 80/20 con `random_state=42`.
- Selección del predictor de la regresión simple basada únicamente en correlaciones de entrenamiento.
- `StandardScaler` ajustado únicamente con entrenamiento.
- GridSearchCV con 5 folds restringido al conjunto de entrenamiento.
- Test reservado hasta finalizar el ajuste.
- Métricas: MSE, RMSE y R².
- Selección final de la corrida: **MLPRegressor**.

## Clasificación

- Dataset: Titanic.
- Objetivo binario: `survived`.
- Predictores: `pclass`, `age`, `sibsp`, `parch`, `fare`, `sex`, `embarked`.
- `alive` excluida por fuga de información respecto de `survived`.
- `class` y `embark_town` excluidas por redundancia.
- `who`, `adult_male` y `alone` excluidas por ser variables derivadas.
- `deck` excluida por alta ausencia.
- Se conservaron las 891 observaciones canónicas; las 107 filas exactamente repetidas no se eliminaron porque no existe identificador único que permita demostrar duplicación de individuos.
- Split estratificado 80/20 antes de imputación, codificación y escalamiento.
- Preprocesamiento ajustado exclusivamente con entrenamiento.
- Arquitecturas MLP: `(100,)`, `(100, 50)`, `(100, 50, 25)`.
- Los demás hiperparámetros se mantuvieron constantes para aislar la comparación arquitectónica.
- Métricas: accuracy, precision, recall, F1, balanced accuracy, especificidad y matriz de confusión.
- Selección final de la corrida: **MLP de dos capas ocultas `(100, 50)`** bajo criterio de desempeño equilibrado.
