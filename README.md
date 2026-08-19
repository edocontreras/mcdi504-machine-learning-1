# MCDI504 · Machine Learning I
## Grupo 6

**Integrantes:** Luis Díaz Giral, Gonzalo Bouldres y Eduardo Contreras  
**Docente:** Dr. David Ruete Zúñiga  
**Programa:** Magíster en Ciencia de Datos e Inteligencia Artificial  
**Universidad:** Universidad Andrés Bello

## Evaluación Sumativa 2 · Semana 3

Repositorio consolidado del proyecto ABP que integra:

- **RA2:** regresión supervisada y evaluación mediante MSE, RMSE y R².
- **RA3:** clasificación supervisada mediante redes neuronales superficiales, matrices de confusión y métricas de clasificación.

Las carpetas `Semana1/` y `Semana2/` se preservan como evidencia histórica. `Semana3/` contiene la corrida ejecutada, sus tablas, figuras, documentación e informe final.

## Estado de la corrida archivada

- Notebook: `Semana3/notebook/F3_RedesNeuronales.ipynb`
- Celdas de código ejecutadas: **15/15**
- Errores de ejecución: **0**
- Control final del notebook: **Validación de artefactos: OK**
- `random_state`: **42**
- Registros California Housing: **20.640**
- Registros Titanic: **891**

## Resultados principales

### Regresión

El **MLPRegressor** presentó el mejor desempeño de prueba de los modelos comparados:

- RMSE test: **0.549301**
- R² test: **0.769742**
- Gap R² train-test: **0.020083**

El ajuste del árbol mediante GridSearchCV redujo RMSE en **16.80%** respecto de la configuración inicial. La configuración seleccionada fue `max_depth=12`, `min_samples_leaf=10` y `min_samples_split=2`.

### Clasificación

Las arquitecturas evaluadas fueron `(100,)`, `(100, 50)` y `(100, 50, 25)`.

El **MLP con dos capas ocultas** obtuvo el mejor desempeño global equilibrado en esta corrida:

- Accuracy: **0.793296**
- Recall: **0.724638**
- F1-score: **0.729927**
- Balanced accuracy: **0.780501**
- Falsos negativos: **19**

La arquitectura de tres capas presentó la mayor precision y especificidad, pero menor recall y mayor brecha F1 train-test.

## Reproducibilidad

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

Abrir `Semana3/notebook/F3_RedesNeuronales.ipynb`, reiniciar el kernel y ejecutar todas las celdas en orden. El notebook regenera `Semana3/outputs/` y `Semana3/figures/`.

## Estructura de Semana 3

```text
Semana3/
├── data/
├── notebook/
│   └── F3_RedesNeuronales.ipynb
├── outputs/
├── figures/
├── docs/
└── informe/
    ├── f3_s03_grupo6.docx
    └── f3_s03_grupo6.pdf
```
