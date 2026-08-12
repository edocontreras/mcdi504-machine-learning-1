# MCDI504 · Machine Learning I
## Proyecto ABP · Grupo 6

**Docente:** Dr. David Ruete Zúñiga  
**Integrantes:** Luis Díaz Giral, Gonzalo Bouldres y Eduardo Contreras  
**Programa:** Magíster en Ciencia de Datos e Inteligencia Artificial  
**Universidad:** Universidad Andrés Bello

## Estructura del repositorio

```text
mcdi504-machine-learning-1/
├── Semana1/
├── Semana2/
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Semana 1 · Fase 1: Definición y orientación de la situación

**Proyecto:** IrisFlow  
**Fecha de entrega:** 08-08-2026

La primera fase documenta la definición analítica del problema, la caracterización inicial del conjunto Iris, el análisis exploratorio, el preprocesamiento básico y su relación con el proceso KDD.

Principales evidencias:

- `Semana1/notebook/F1_Definicion.ipynb`
- `Semana1/data/`
- `Semana1/outputs/`
- `Semana1/figures/`
- `Semana1/docs/`
- `Semana1/informe/MCDI504_S1_1_GRUPO6.pdf`

## Semana 2 · Fase 2: Búsqueda y recopilación de información

**Caso de regresión:** California Housing  
**Variable objetivo:** `MedHouseVal`  
**Fecha de entrega:** 14-08-2026

La segunda fase desarrolla la preparación analítica del conjunto de datos y la implementación de modelos de regresión supervisada. El flujo incluye:

1. descripción de California Housing y definición de la variable objetivo;
2. control de valores faltantes y análisis exploratorio;
3. partición entrenamiento/prueba 80/20 con `random_state=42`;
4. selección del predictor para regresión lineal simple utilizando exclusivamente el conjunto de entrenamiento;
5. estandarización mediante `StandardScaler` ajustado con `X_train`;
6. regresión lineal simple;
7. árbol de decisión para regresión;
8. red neuronal MLP;
9. evaluación mediante MSE, RMSE y R²;
10. comparación de modelos y diagnóstico de generalización.

Principales evidencias:

- `Semana2/notebook/F2_Regresion.ipynb`
- `Semana2/outputs/`
- `Semana2/figures/`
- `Semana2/docs/`
- `Semana2/informe/MCDI504_S2_1_GRUPO6.pdf`

## Reproducción

Instalar las dependencias desde la raíz del repositorio:

```bash
pip install -r requirements.txt
```

Luego iniciar Jupyter:

```bash
jupyter notebook
```

Para reproducir la Fase 2, abrir `Semana2/notebook/F2_Regresion.ipynb` y ejecutar las celdas secuencialmente desde el inicio. La primera carga de California Housing puede requerir conexión a Internet si el conjunto no está disponible en la caché local de scikit-learn.
