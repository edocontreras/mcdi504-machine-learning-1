# MCDI504 · Machine Learning I

## Proyecto ABP · Grupo 6

**Integrantes:** Luis Díaz Giral, Gonzalo Bouldres y Eduardo Contreras  
**Docente:** Dr. David Ruete Zúñiga  
**Programa:** Magíster en Ciencia de Datos e Inteligencia Artificial  
**Universidad:** Universidad Andrés Bello  
**Asignatura:** MCDI504 · Machine Learning I  

---

## 1. Descripción del repositorio

Este repositorio reúne el desarrollo progresivo del proyecto ABP de **Machine Learning I** durante las **Semanas 1, 2 y 3**.

La organización conserva cada fase como una unidad trazable e independiente, con su notebook ejecutado, evidencia tabular, visualizaciones, documentación técnica e informe correspondiente.

La progresión general del proyecto es:

```text
Semana 1
Definición y orientación de la situación
Clasificación supervisada multiclase · Iris
        ↓
Semana 2
Búsqueda y recopilación de información
Regresión supervisada · California Housing
        ↓
Semana 3
Evaluación Sumativa 2 · Integración Fases 2 y 3
Regresión supervisada + clasificación mediante redes neuronales
```

Las carpetas `Semana1/` y `Semana2/` se mantienen como **evidencia histórica de las fases ya desarrolladas**. `Semana3/` consolida la evaluación integrada de los resultados de aprendizaje **RA2 y RA3**.

---

## 2. Estructura general

```text
mcdi504-machine-learning-1/
├── Semana1/
│   ├── data/
│   ├── docs/
│   ├── figures/
│   ├── informe/
│   ├── notebook/
│   └── outputs/
├── Semana2/
│   ├── data/
│   ├── docs/
│   ├── figures/
│   ├── informe/
│   ├── notebook/
│   └── outputs/
├── Semana3/
│   ├── data/
│   ├── docs/
│   ├── figures/
│   ├── informe/
│   ├── notebook/
│   ├── outputs/
│   └── README.md
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

Cada semana mantiene la misma lógica de trazabilidad:

```text
datos
  ↓
notebook ejecutado
  ↓
outputs tabulados
  ↓
figuras
  ↓
decisiones técnicas
  ↓
informe
```

---

# 3. Semana 1 · Fase 1: Definición y orientación de la situación

## 3.1 Propósito

La primera fase corresponde a la **definición analítica del problema**, caracterización del conjunto de datos y justificación del tipo de aprendizaje.

El caso se desarrolla bajo el escenario **IrisFlow**, utilizando el dataset clásico **Iris** para formular un problema de **clasificación supervisada multiclase**.

En esta fase **no se entrenan ni evalúan modelos predictivos**. El alcance está centrado en establecer si la estructura y calidad de los datos permiten formular de manera consistente el problema de Machine Learning.

## 3.2 Dataset

El notebook carga el dataset mediante:

```python
sklearn.datasets.load_iris()
```

La ejecución exporta una copia trazable a:

```text
Semana1/data/iris_original.csv
```

### Características

- **150 observaciones**
- **4 variables predictoras continuas**
- **1 variable objetivo categórica nominal**
- **3 clases**
- **50 observaciones por clase**

### Variables

| Variable | Rol | Tipo |
|---|---|---|
| `Sepal.Length` | Predictora | Numérica continua |
| `Sepal.Width` | Predictora | Numérica continua |
| `Petal.Length` | Predictora | Numérica continua |
| `Petal.Width` | Predictora | Numérica continua |
| `Species` | Objetivo | Categórica nominal |

Clases de `Species`:

```text
setosa
versicolor
virginica
```

## 3.3 Trabajo desarrollado

La Fase 1 incluye:

- formulación del problema analítico;
- identificación del tipo de aprendizaje;
- relación entre Machine Learning y metodología KDD;
- carga y estructura del dataset;
- diccionario de variables;
- control de integridad;
- distribución de clases;
- estadística descriptiva;
- identificación de valores atípicos mediante criterio de Tukey;
- codificación temporal de `Species` con fines exclusivamente exploratorios;
- correlación de Pearson entre predictores continuos;
- valores p asociados a Pearson;
- normalización Min-Max de predictores;
- comparación conceptual entre enfoques de aprendizaje;
- documentación de decisiones técnicas y trazabilidad.

## 3.4 Decisiones metodológicas relevantes

- `Species` se mantiene como variable objetivo categórica nominal.
- La codificación numérica de `Species` se utiliza solo como apoyo exploratorio y no se interpreta como escala ordinal.
- Los índices 101 y 142 presentan combinaciones de valores coincidentes; se conservan porque la información disponible no permite establecer que correspondan a una misma unidad experimental.
- El criterio de Tukey detecta cuatro valores atípicos relativos en `Sepal.Width`; no se eliminan automáticamente.
- La inferencia de Pearson se restringe a los predictores continuos.
- La normalización Min-Max se aplica exclusivamente a los predictores.
- No se realiza split, entrenamiento, ajuste de hiperparámetros ni evaluación predictiva en esta fase.

## 3.5 Estado del notebook

```text
Notebook: Semana1/notebook/F1_Definicion.ipynb
Celdas de código: 22
Celdas ejecutadas: 22/22
Errores almacenados: 0
```

## 3.6 Evidencia principal

- [Notebook F1_Definicion.ipynb](Semana1/notebook/F1_Definicion.ipynb)
- [Informe Fase 1](Semana1/informe/MCDI504_S1_1_GRUPO6.pdf)
- [Decisiones técnicas](Semana1/docs/DECISIONES_TECNICAS.md)
- [Fuentes](Semana1/docs/FUENTES.md)
- [Trazabilidad](Semana1/docs/TRAZABILIDAD.md)
- [Datos](Semana1/data/)
- [Outputs](Semana1/outputs/)
- [Figuras](Semana1/figures/)

---

# 4. Semana 2 · Fase 2: Búsqueda y recopilación de información

## 4.1 Propósito

La segunda fase desarrolla un problema de **regresión supervisada** utilizando **California Housing**.

El objetivo es predecir la variable continua `MedHouseVal` y comparar modelos con diferentes capacidades de representación.

## 4.2 Dataset

La carga utilizada en el notebook es:

```python
sklearn.datasets.fetch_california_housing(as_frame=True)
```

### Características

- **20.640 observaciones**
- **8 variables predictoras numéricas**
- **Variable objetivo continua:** `MedHouseVal`
- **Valores faltantes:** 0 en la carga utilizada

### Predictores

```text
MedInc
HouseAge
AveRooms
AveBedrms
Population
AveOccup
Latitude
Longitude
```

> **Nota de reproducibilidad:** en Semana 2 el dataset se obtiene mediante `fetch_california_housing`. Una primera ejecución puede requerir acceso a Internet si California Housing no se encuentra previamente en la caché local de scikit-learn. En Semana 3 se incorpora una copia local para asegurar la reproducibilidad de la evaluación integrada.

## 4.3 Preparación analítica

- partición **80% entrenamiento / 20% prueba**;
- `random_state=42`;
- verificación de valores faltantes;
- análisis descriptivo;
- matriz de correlaciones;
- selección del predictor de la regresión lineal simple **exclusivamente sobre entrenamiento**;
- `StandardScaler` ajustado únicamente con `X_train`;
- transformación posterior de entrenamiento y prueba con parámetros aprendidos desde train.

El predictor seleccionado para la regresión lineal simple es:

```text
MedInc
```

## 4.4 Modelos

Se implementan tres modelos principales:

1. **Regresión lineal simple**
2. **DecisionTreeRegressor**
3. **MLPRegressor**

Además, se conserva una **regresión lineal multivariable** como comparación complementaria usando los ocho predictores.

### Configuraciones principales

**Árbol de decisión**

```text
max_depth = 5
random_state = 42
```

**MLPRegressor**

```text
hidden_layer_sizes = (100,)
activation = relu
solver = adam
max_iter = 500
early_stopping = True
random_state = 42
```

## 4.5 Métricas

Todos los modelos se evalúan sobre el mismo conjunto de prueba utilizando:

- **MSE**
- **RMSE**
- **R²**

### Resultados principales

| Modelo | MSE | RMSE | R² |
|---|---:|---:|---:|
| Regresión lineal simple (`MedInc`) | 0.709116 | 0.842090 | 0.458859 |
| Árbol de decisión | 0.524515 | 0.724234 | 0.599732 |
| **Red neuronal MLP** | **0.301732** | **0.549301** | **0.769742** |

### Comparación complementaria

| Modelo | MSE | RMSE | R² |
|---|---:|---:|---:|
| Regresión lineal multivariable | 0.555892 | 0.745581 | 0.575788 |
| Árbol de decisión | 0.524515 | 0.724234 | 0.599732 |
| **Red neuronal MLP** | **0.301732** | **0.549301** | **0.769742** |

En la corrida archivada, el **MLPRegressor** presenta el menor error de prueba y el mayor R².

## 4.6 Diagnóstico de generalización

La fase también compara desempeño entre entrenamiento y prueba mediante RMSE y R², evitando seleccionar un modelo exclusivamente por una métrica aislada de test.

## 4.7 Estado del notebook

```text
Notebook: Semana2/notebook/F2_Regresion.ipynb
Celdas de código: 16
Celdas ejecutadas: 16/16
Errores almacenados: 0
```

## 4.8 Evidencia principal

- [Notebook F2_Regresion.ipynb](Semana2/notebook/F2_Regresion.ipynb)
- [Informe Fase 2](Semana2/informe/MCDI504_S2_1_GRUPO6.pdf)
- [Decisiones técnicas](Semana2/docs/DECISIONES_TECNICAS.md)
- [Fuentes](Semana2/docs/FUENTES.md)
- [Trazabilidad](Semana2/docs/TRAZABILIDAD.md)
- [Información del dataset](Semana2/data/README.md)
- [Outputs](Semana2/outputs/)
- [Figuras](Semana2/figures/)

---

# 5. Semana 3 · Evaluación Sumativa 2: Informe final de proyecto · Fases 2 y 3

## 5.1 Propósito

La tercera semana integra los resultados de aprendizaje:

- **RA2:** regresión supervisada;
- **RA3:** clasificación supervisada.

La evaluación reúne **informe técnico + notebook + repositorio** como componentes de un mismo flujo reproducible.

La evidencia computacional se concentra en:

1. consolidación de la regresión de Fase 2;
2. ajuste explícito de hiperparámetros de regresión;
3. preparación y análisis exploratorio de un problema de clasificación;
4. implementación de redes neuronales con una, dos y tres capas ocultas;
5. matrices de confusión y métricas;
6. comparación técnica de arquitecturas;
7. selección fundamentada de los modelos más pertinentes.

---

## 5.2 Parte A · Regresión supervisada

### Dataset

Se utiliza nuevamente **California Housing**, ahora mediante copia local:

```text
Semana3/data/california_housing.csv
```

Esto permite que la ejecución de Semana 3 no dependa de una descarga externa.

### Preparación

- 20.640 observaciones;
- 8 predictores;
- objetivo continuo `MedHouseVal`;
- 0 valores faltantes;
- split 80/20;
- `random_state=42`;
- selección del predictor simple únicamente con train;
- escalamiento aprendido únicamente con train.

### Modelos comparados

- regresión lineal simple;
- regresión lineal multivariable;
- árbol inicial;
- MLPRegressor;
- árbol ajustado.

## 5.3 Ajuste de hiperparámetros

El ajuste se realiza sobre `DecisionTreeRegressor` mediante:

```text
GridSearchCV
5 folds
72 configuraciones
```

Hiperparámetros evaluados:

```text
max_depth
min_samples_split
min_samples_leaf
```

La búsqueda utiliza exclusivamente el conjunto de entrenamiento.

### Configuración seleccionada

```text
max_depth = 12
min_samples_leaf = 10
min_samples_split = 2
```

## 5.4 Resultados finales de regresión

| Modelo | MSE test | RMSE test | R² test |
|---|---:|---:|---:|
| Regresión lineal simple | 0.709116 | 0.842090 | 0.458859 |
| Regresión lineal multivariable | 0.555892 | 0.745581 | 0.575788 |
| Árbol inicial | 0.524515 | 0.724234 | 0.599732 |
| **MLP regresión** | **0.301732** | **0.549301** | **0.769742** |
| Árbol ajustado | 0.363096 | 0.602575 | 0.722914 |

El ajuste del árbol reduce su RMSE respecto de la configuración inicial, pero el **MLPRegressor** mantiene el mejor desempeño predictivo global en la corrida archivada.

---

# 6. Semana 3 · Parte B: clasificación supervisada

## 6.1 Dataset

Se utiliza una copia local de **Titanic**:

```text
Semana3/data/titanic.csv
```

### Características

- **891 observaciones**
- objetivo binario: `survived`
- clase `0`: no sobrevivió
- clase `1`: sobrevivió

### Predictores seleccionados

```text
pclass
age
sibsp
parch
fare
sex
embarked
```

## 6.2 Selección de variables

Se documentan explícitamente las exclusiones:

- `alive`: fuga directa de información respecto de `survived`;
- `class`: redundante con `pclass`;
- `embark_town`: redundante con `embarked`;
- `who`, `adult_male`, `alone`: variables derivadas;
- `deck`: alta proporción de valores faltantes.

La ejecución detecta **107 filas exactamente repetidas** considerando las variables disponibles. Se conservan porque el dataset no dispone de un identificador único que permita demostrar que correspondan al mismo individuo.

## 6.3 Análisis exploratorio

El EDA considera:

- distribución de clases;
- diagnóstico de balance;
- valores faltantes;
- patrones por `sex`;
- patrones por `pclass`;
- patrones por `embarked`;
- comportamiento de `age`;
- comportamiento de `fare`;
- `sibsp`;
- `parch`.

La clase objetivo presenta un desbalance moderado, por lo que la evaluación no se limita a accuracy.

## 6.4 Preprocesamiento

La secuencia evita utilizar información del conjunto de prueba para aprender transformaciones:

```text
dataset
   ↓
selección X / y
   ↓
train_test_split con stratify
   ↓
imputación ajustada con train
   ↓
One-Hot Encoding ajustado con train
   ↓
StandardScaler ajustado con train
   ↓
transformación de train y test
   ↓
entrenamiento de redes
```

El control posterior al preprocesamiento registra:

```text
NaN en train = 0
NaN en test  = 0
```

---

# 7. Arquitecturas de redes neuronales

Las tres arquitecturas se implementan mediante `MLPClassifier`.

| Modelo | Capas ocultas |
|---|---|
| MLP 1 capa | `(100,)` |
| MLP 2 capas | `(100, 50)` |
| MLP 3 capas | `(100, 50, 25)` |

Para aislar el efecto de la arquitectura, los demás hiperparámetros se mantienen constantes:

```text
activation = relu
solver = adam
alpha = 0.0001
learning_rate_init = 0.001
max_iter = 500
early_stopping = True
validation_fraction = 0.15
n_iter_no_change = 20
random_state = 42
```

---

# 8. Evaluación de clasificación

Para cada arquitectura se calculan:

- matriz de confusión;
- accuracy;
- precision;
- recall;
- F1-score;
- balanced accuracy;
- especificidad;
- TN;
- FP;
- FN;
- TP;
- pérdida final;
- iteraciones;
- parámetros entrenables;
- desempeño train/test;
- brechas de generalización.

## 8.1 Resultados

| Arquitectura | Accuracy | Precision | Recall | F1 | Balanced accuracy |
|---|---:|---:|---:|---:|---:|
| MLP 1 capa | 0.776536 | 0.754386 | 0.623188 | 0.682540 | 0.747958 |
| **MLP 2 capas** | **0.793296** | 0.735294 | **0.724638** | **0.729927** | **0.780501** |
| MLP 3 capas | 0.787709 | **0.816327** | 0.579710 | 0.677966 | 0.748946 |

### Matrices de confusión

**MLP 1 capa**

```text
TN = 96
FP = 14
FN = 26
TP = 43
```

**MLP 2 capas**

```text
TN = 92
FP = 18
FN = 19
TP = 50
```

**MLP 3 capas**

```text
TN = 101
FP = 9
FN = 29
TP = 40
```

## 8.2 Selección final

Bajo un criterio de desempeño global equilibrado, la arquitectura seleccionada es:

```text
MLPClassifier
hidden_layer_sizes = (100, 50)
```

La red de dos capas presenta:

- mayor accuracy;
- mayor recall;
- mayor F1-score;
- mayor balanced accuracy;
- menor número de falsos negativos.

La red de tres capas obtiene mayor precision y especificidad, pero reduce el recall y presenta una brecha de generalización mayor.

La selección se fundamenta en el conjunto de métricas y no en accuracy de manera aislada.

---

# 9. Estado técnico de Semana 3

```text
Notebook: Semana3/notebook/F3_RedesNeuronales.ipynb
Celdas totales: 31
Celdas de código: 15
Celdas ejecutadas: 15/15
Errores almacenados: 0
Control final: Validación de artefactos: OK
Figuras generadas: 15
```

El notebook genera automáticamente tablas, figuras, controles de consistencia y manifiestos de artefactos.

---

# 10. Evidencia principal de Semana 3

- [README Semana 3](Semana3/README.md)
- [Notebook F3_RedesNeuronales.ipynb](Semana3/notebook/F3_RedesNeuronales.ipynb)
- [Informe final PDF](Semana3/informe/f3_s03_grupo6.pdf)
- [Informe final DOCX](Semana3/informe/f3_s03_grupo6.docx)
- [Decisiones metodológicas](Semana3/docs/DECISIONES_METODOLOGICAS.md)
- [Resultados y decisiones](Semana3/docs/RESULTADOS_Y_DECISIONES.md)
- [Trazabilidad de la rúbrica](Semana3/docs/TRAZABILIDAD_RUBRICA.md)
- [Auditoría final](Semana3/docs/AUDITORIA_FINAL.md)
- [Fuentes base](Semana3/docs/FUENTES_BASE.md)
- [Guía de ejecución](Semana3/docs/GUIA_EJECUCION.md)
- [Manifiesto final](Semana3/docs/MANIFIESTO_REPOSITORIO_FINAL.csv)
- [Datos](Semana3/data/)
- [Outputs](Semana3/outputs/)
- [Figuras](Semana3/figures/)

---

# 11. Resumen de la evolución del proyecto

| Semana | Fase | Dataset | Problema | Evidencia principal |
|---|---|---|---|---|
| 1 | Definición y orientación | Iris | Clasificación multiclase · formulación y EDA | KDD, calidad, correlaciones, normalización |
| 2 | Búsqueda y recopilación | California Housing | Regresión supervisada | Lineal, árbol, MLP, MSE/RMSE/R² |
| 3 | Evaluación Sumativa 2 | California Housing + Titanic | Regresión + clasificación | Tuning, 3 MLP, matrices, comparación y selección |

---

# 12. Reproducibilidad

## 12.1 Dependencias

Desde la raíz del repositorio:

```bash
python -m pip install -r requirements.txt
```

El archivo `requirements.txt` contiene:

```text
numpy==1.26.4
pandas==2.2.2
matplotlib==3.8.4
scikit-learn==1.4.2
seaborn==0.13.2
scipy>=1.11,<2
notebook>=7,<8
ipykernel>=6,<8
```

## 12.2 Inicio de Jupyter

```bash
jupyter notebook
```

## 12.3 Notebooks principales

```text
Semana1/notebook/F1_Definicion.ipynb
Semana2/notebook/F2_Regresion.ipynb
Semana3/notebook/F3_RedesNeuronales.ipynb
```

Para reproducir una corrida:

1. abrir el notebook correspondiente;
2. reiniciar el kernel;
3. ejecutar todas las celdas en orden;
4. verificar que no existan errores;
5. guardar el notebook después de la ejecución.

### Consideraciones sobre los datos

- **Semana 1:** `load_iris()` está incluido en scikit-learn; además se conserva `iris_original.csv`.
- **Semana 2:** `fetch_california_housing()` puede requerir acceso a Internet en una primera ejecución si el dataset no está en caché.
- **Semana 3:** California Housing y Titanic están almacenados localmente dentro de `Semana3/data/`.

---

# 13. Convenciones metodológicas transversales

A lo largo del proyecto se mantienen los siguientes principios:

- separación entre variable objetivo y predictores;
- documentación explícita de decisiones técnicas;
- control de valores faltantes y consistencia de datos;
- preservación del conjunto de prueba para evaluación;
- ajuste de transformaciones utilizando únicamente entrenamiento cuando corresponde;
- uso de `random_state=42` para reproducibilidad;
- métricas coherentes con el tipo de problema;
- comparación sobre conjuntos de prueba comunes;
- análisis de generalización;
- trazabilidad entre notebook, outputs, figuras, documentación e informe;
- conservación de la evidencia histórica de cada fase.

---

# 14. Informes

| Semana | Informe |
|---|---|
| Semana 1 | [`MCDI504_S1_1_GRUPO6.pdf`](Semana1/informe/MCDI504_S1_1_GRUPO6.pdf) |
| Semana 2 | [`MCDI504_S2_1_GRUPO6.pdf`](Semana2/informe/MCDI504_S2_1_GRUPO6.pdf) |
| Semana 3 | [`f3_s03_grupo6.pdf`](Semana3/informe/f3_s03_grupo6.pdf) |

---

# 15. Licencia

Este repositorio utiliza la **MIT License**.

Consultar:

[LICENSE](LICENSE)
