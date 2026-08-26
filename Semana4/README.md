# Semana 4 · Fase 4 · Evaluación y validación del modelo

Estado: **Evaluación Formativa 4 y Evaluación Sumativa 3 ejecutadas, documentadas y auditadas**.

## Propósito general de la Semana 4

La Semana 4 corresponde a la Fase 4 del proyecto ABP de la asignatura MCDI504 · Machine Learning I. Su propósito es evaluar cuantitativamente el desempeño de los modelos supervisados desarrollados durante el proyecto, analizar sus errores de clasificación, estudiar la estabilidad de las métricas mediante validación cruzada y fundamentar decisiones metodológicas orientadas a la selección y validación del modelo.

La semana contiene dos entregables complementarios:

1. **Evaluación Formativa 4 · Avance de la Fase 4 (`S4_1`)**  
   Evalúa comparativamente los modelos supervisados implementados previamente y aplica validación cruzada a una red neuronal con una capa oculta.

2. **Evaluación Sumativa 3 · Cierre de la Fase 4 (`S4_2`)**  
   Evalúa y valida en profundidad el modelo MLP de dos capas ocultas seleccionado al cierre de Semana 3.

Ambos entregables se mantienen separados para conservar la trazabilidad de notebooks, resultados, figuras, documentación e informes.

---

## Estructura de Semana 4

```text
Semana4/
├── Formativa/                  # Evaluación Formativa 4 · S4_1
│   ├── data/
│   ├── docs/
│   ├── figures/
│   ├── informe/
│   ├── notebook/
│   ├── outputs/
│   └── README.md
│
├── data/                       # Evaluación Sumativa 3 · S4_2
├── docs/
├── figures/
├── informe/
├── notebook/
├── outputs/
└── README.md
```

La carpeta `Formativa/` contiene exclusivamente la evidencia correspondiente a la Evaluación Formativa 4. Las carpetas restantes de `Semana4/` corresponden a la Evaluación Sumativa 3.

---

# 1. Evaluación Formativa 4 · Avance de la Fase 4

Estado: **ejecución final archivada, verificada y documentada**.

## 1.1 Propósito

La Evaluación Formativa 4 desarrolla una evaluación preliminar y comparativa de los modelos supervisados de clasificación utilizados en el proyecto para el caso Titanic.

La fase permite:

- evaluar el desempeño de diferentes clasificadores bajo una misma partición Hold-Out;
- calcular matrices de confusión y métricas de clasificación;
- interpretar falsos positivos y falsos negativos;
- comparar fortalezas y limitaciones de los modelos;
- aplicar validación cruzada a una red neuronal con una capa oculta;
- analizar la estabilidad de las métricas entre folds;
- relacionar tamaño del conjunto de datos, costo computacional y estabilidad;
- generar evidencia reproducible para sustentar las decisiones del informe.

---

## 1.2 Dataset

El análisis utiliza el dataset Titanic archivado en el proyecto.

- Observaciones totales: **891**.
- Variable objetivo: `survived`.
- Clase negativa: `0` = no sobrevivió.
- Clase positiva: `1` = sobrevivió.
- Observaciones clase 0: **549**.
- Observaciones clase 1: **342**.

Distribución aproximada:

| Clase | Observaciones | Proporción |
|---|---:|---:|
| No sobrevivió (`0`) | 549 | 61.62 % |
| Sobrevivió (`1`) | 342 | 38.38 % |

Predictores utilizados:

- `pclass`
- `age`
- `sibsp`
- `parch`
- `fare`
- `sex`
- `embarked`

La copia canónica del dataset se mantiene en:

```text
Semana3/data/titanic.csv
```

La carpeta `Formativa/data/` documenta su procedencia y uso dentro de esta evaluación.

---

## 1.3 Partición Hold-Out

La evaluación utiliza una partición estratificada:

```python
train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42,
    stratify=y
)
```

Dimensiones:

- Entrenamiento: **712 observaciones**.
- Prueba: **179 observaciones**.

La estratificación preserva aproximadamente la proporción de ambas clases entre entrenamiento y prueba.

---

## 1.4 Preprocesamiento

El preprocesamiento se implementa mediante `Pipeline` y `ColumnTransformer`.

Variables numéricas:

- imputación de datos faltantes;
- estandarización cuando el algoritmo lo requiere.

Variables categóricas:

- imputación de datos faltantes;
- One-Hot Encoding.

Para los modelos sensibles a escala, el escalamiento se incorpora dentro del pipeline del modelo.

En validación cruzada, el pipeline se reajusta independientemente dentro de cada fold. De esta manera, imputación, codificación y escalamiento se estiman únicamente a partir de la porción de entrenamiento correspondiente a cada partición.

---

## 1.5 Modelos evaluados

La comparación Hold-Out considera siete clasificadores:

1. K-Nearest Neighbors.
2. Árbol de decisión.
3. Support Vector Machine con kernel RBF.
4. Gaussian Naive Bayes.
5. MLP con una capa oculta.
6. MLP con dos capas ocultas.
7. MLP con tres capas ocultas.

Arquitecturas MLP:

```text
MLP 1 capa:  hidden_layer_sizes=(100,)
MLP 2 capas: hidden_layer_sizes=(100, 50)
MLP 3 capas: hidden_layer_sizes=(100, 50, 25)
```

Las configuraciones de las redes neuronales mantienen continuidad con las arquitecturas documentadas en Semana 3.

---

## 1.6 Métricas utilizadas

Métricas principales:

- Accuracy.
- Precision.
- Recall.
- F1-score.

Métricas complementarias:

- Balanced accuracy.
- Especificidad.
- False Positive Rate.
- False Negative Rate.
- ROC-AUC.
- Average Precision.

La clase positiva utilizada para precision, recall y F1-score es:

```text
survived = 1
```

---

## 1.7 Resultados Hold-Out

| Modelo | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| KNN | 0.8156 | 0.8103 | 0.6812 | 0.7402 | 0.8353 |
| Árbol de decisión | 0.7654 | 0.7547 | 0.5797 | 0.6557 | 0.7971 |
| **SVM** | **0.8324** | **0.8305** | 0.7101 | **0.7656** | 0.8337 |
| Naive Bayes | 0.7821 | 0.7273 | 0.6957 | 0.7111 | 0.8080 |
| MLP 1 capa | 0.7765 | 0.7544 | 0.6232 | 0.6825 | 0.8360 |
| MLP 2 capas | 0.7933 | 0.7353 | **0.7246** | 0.7299 | **0.8522** |
| MLP 3 capas | 0.7877 | 0.8163 | 0.5797 | 0.6780 | 0.8370 |

La comparación muestra que:

- SVM alcanza la mayor accuracy Hold-Out.
- SVM presenta también el mayor F1-score.
- El MLP de dos capas obtiene el mayor recall.
- El MLP de dos capas alcanza el mayor ROC-AUC.
- La selección no debe reducirse a una única métrica.

---

## 1.8 Errores de clasificación

En clasificación binaria se utiliza la convención:

```text
TN = verdadero negativo
FP = falso positivo
FN = falso negativo
TP = verdadero positivo
```

Los errores FP y FN se analizan explícitamente porque representan tipos de error diferentes.

Cuando el objetivo es detectar correctamente sobrevivientes reales, el recall y los falsos negativos adquieren especial importancia.

Cuando la prioridad es aumentar la confiabilidad de una predicción positiva, la precision y los falsos positivos tienen mayor relevancia.

---

# 2. Validación cruzada del MLP de una capa oculta

La Evaluación Formativa exige específicamente aplicar validación cruzada a una red neuronal con una capa oculta.

El modelo validado es:

```python
MLPClassifier(hidden_layer_sizes=(100,))
```

---

## 2.1 Técnica utilizada

Se utiliza:

```python
StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)
```

La validación se ejecuta exclusivamente sobre las **712 observaciones del conjunto de entrenamiento**.

El conjunto de prueba Hold-Out no participa en el ajuste de los folds.

---

## 2.2 Resultados por fold

| Fold | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---:|---:|---:|---:|---:|---:|
| 1 | 0.8042 | 0.7647 | 0.7091 | 0.7358 | 0.8658 |
| 2 | 0.7972 | 0.7955 | 0.6364 | 0.7071 | 0.8292 |
| 3 | 0.8310 | 0.8780 | 0.6545 | 0.7500 | 0.8730 |
| 4 | 0.7887 | 0.7222 | 0.7222 | 0.7222 | 0.8480 |
| 5 | 0.8169 | 0.8500 | 0.6296 | 0.7234 | 0.8693 |

---

## 2.3 Estabilidad de las métricas

| Métrica | Promedio CV | Desv. estándar muestral |
|---|---:|---:|
| Accuracy | **0.8076** | **0.0167** |
| Precision | 0.8021 | 0.0630 |
| Recall | 0.6704 | 0.0426 |
| F1-score | **0.7277** | **0.0161** |
| Balanced accuracy | 0.7817 | 0.0118 |
| ROC-AUC | **0.8571** | **0.0183** |
| Average precision | 0.8237 | 0.0191 |

La variabilidad observada no es uniforme para todas las métricas.

Accuracy, F1-score y ROC-AUC presentan dispersiones relativamente bajas entre folds. Precision y recall muestran una sensibilidad mayor a la composición de las particiones.

---

## 2.4 Matriz de confusión OOF agregada

Las predicciones out-of-fold producen:

```text
TN = 392
FP = 47
FN = 90
TP = 183
```

Matriz:

```text
[[392, 47],
 [ 90, 183]]
```

La suma es:

```text
392 + 47 + 90 + 183 = 712
```

correspondiente exactamente al tamaño del conjunto de entrenamiento.

---

## 2.5 Controles OOF

La ejecución verifica automáticamente:

- cobertura completa de las 712 observaciones de entrenamiento;
- unicidad de los índices OOF;
- ausencia de observaciones del test dentro de las predicciones OOF;
- correspondencia entre predicciones OOF y matriz de confusión agregada.

Controles:

```text
OOF_cubre_todo_train = True
Indices_OOF_unicos = True
OOF_disjunto_test = True
Matriz_agregada_suma_train = True
```

---

# 3. Justificación de la técnica de validación

La elección de K-Fold se fundamenta conjuntamente en:

- tamaño del conjunto de entrenamiento;
- costo computacional;
- necesidad de analizar estabilidad.

Comparación:

| Técnica | Ajustes aproximados del MLP | Costo relativo | Característica |
|---|---:|---|---|
| Hold-Out | 1 | Bajo | Depende de una única partición |
| Stratified K-Fold k=5 | 5 | Medio | Permite estimar estabilidad |
| Leave-One-Out | 712 | Alto | Elevado costo computacional |

Para las 712 observaciones de entrenamiento, K-Fold con cinco particiones constituye un compromiso entre costo computacional y repetición de la estimación.

El notebook registra además el tiempo de entrenamiento observado durante la validación cruzada como evidencia de reproducibilidad. Dicho tiempo depende del hardware y del entorno de ejecución y no se interpreta como una propiedad intrínseca del algoritmo.

---

# 4. Comparación Hold-Out y validación cruzada

Para el MLP de una capa:

| Métrica | Hold-Out | Promedio CV |
|---|---:|---:|
| Accuracy | 0.7765 | 0.8076 |
| Precision | 0.7544 | 0.8021 |
| Recall | 0.6232 | 0.6704 |
| F1-score | 0.6825 | 0.7277 |
| ROC-AUC | 0.8360 | 0.8571 |
| Average precision | 0.7557 | 0.8237 |

La partición Hold-Out produce resultados más conservadores que el promedio de validación cruzada para este modelo.

La diferencia evidencia la dependencia que puede existir respecto de una sola división del dataset y sustenta el uso de K-Fold como herramienta adicional para estudiar estabilidad.

---

# 5. Controles de la Evaluación Formativa

La corrida archivada presenta:

```text
7/7 celdas de código ejecutadas
0 errores almacenados
0 advertencias del MLP en Hold-Out
0 advertencias del MLP en K-Fold
47/47 artefactos requeridos presentes
```

También se verifica:

- continuidad de los tres MLP con Semana 3;
- correspondencia entre matrices y métricas;
- integridad de las predicciones;
- cobertura OOF completa;
- separación entre entrenamiento y test;
- generación correcta de figuras y outputs.

La última celda del notebook informa:

```text
Control final de consistencia: OK
Validación cruzada MLP 1 capa: OK
Artefactos requeridos: OK
```

---

# 6. Evidencia de la Evaluación Formativa

## Notebook

- [F4_Evaluacion.ipynb](Formativa/notebook/F4_Evaluacion.ipynb)

## Informe

- [Informe final PDF · S4_1](Formativa/informe/MCDI504_S4_1_GRUPO6.pdf)
- [Informe editable DOCX · S4_1](Formativa/informe/MCDI504_S4_1_GRUPO6.docx)

## Documentación

- [README de la Formativa](Formativa/README.md)
- [Auditoría final](Formativa/docs/AUDITORIA_FINAL.md)
- [Decisiones metodológicas](Formativa/docs/DECISIONES_METODOLOGICAS.md)
- [Resultados y decisiones](Formativa/docs/RESULTADOS_Y_DECISIONES.md)
- [Trazabilidad de la rúbrica](Formativa/docs/TRAZABILIDAD_RUBRICA.md)
- [Fuentes base](Formativa/docs/FUENTES_BASE.md)
- [Guía de ejecución](Formativa/docs/GUIA_EJECUCION.md)
- [Manifiesto final de la Formativa](Formativa/docs/MANIFIESTO_FORMATIVA_FINAL.csv)

## Evidencia computacional

- [Outputs](Formativa/outputs/)
- [Figuras](Formativa/figures/)

---

# 7. Evaluación Sumativa 3 · Cierre de la Fase 4

Estado: **ejecución final archivada y auditada**.

## 7.1 Propósito

La Evaluación Sumativa 3 evalúa y valida el modelo de clasificación seleccionado al cierre de Semana 3 para el caso Titanic.

El trabajo:

- mantiene continuidad con el proyecto ABP;
- reproduce la partición histórica;
- documenta el desempeño Hold-Out;
- evalúa errores de clasificación;
- incorpora métricas discriminativas;
- estima estabilidad mediante validación cruzada estratificada sobre entrenamiento;
- documenta reproducibilidad y trazabilidad.

---

## 7.2 Contenido

- `data/`: copia verificable del dataset Titanic utilizada por la corrida.
- `notebook/F4_Evaluacion.ipynb`: notebook ejecutado de principio a fin.
- `outputs/`: métricas, predicciones, controles y manifiestos.
- `figures/`: ocho visualizaciones derivadas de la ejecución.
- `docs/`: documentación metodológica y de trazabilidad.
- `informe/`: informe institucional final en DOCX y PDF.

---

## 7.3 Modelo evaluado

- Variable objetivo: `survived`.
- Clase positiva: `1` (`sobrevivió`).
- Predictores:
  - `pclass`
  - `age`
  - `sibsp`
  - `parch`
  - `fare`
  - `sex`
  - `embarked`

Modelo:

```python
MLPClassifier(hidden_layer_sizes=(100, 50))
```

Este modelo corresponde a la arquitectura seleccionada al cierre de Semana 3.

Umbral de clasificación:

```text
0.50
```

El umbral se conserva por continuidad metodológica y no se optimiza utilizando el conjunto test.

---

# 8. Protocolo de evaluación de la Sumativa

- Hold-Out histórico: 80/20 estratificado.
- `random_state=42`.
- Train: 712 observaciones.
- Test: 179 observaciones.

Validación de estabilidad:

```python
StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)
```

La validación se aplica exclusivamente al subconjunto de entrenamiento.

El preprocesamiento utiliza:

- imputación;
- One-Hot Encoding;
- estandarización;
- `Pipeline`.

Cada pipeline se reajusta dentro de cada fold.

---

# 9. Resultados Hold-Out de la Sumativa

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

Matriz:

```text
[[92, 18],
 [19, 50]]
```

---

# 10. Validación cruzada de la Sumativa

| Métrica | Promedio | Desv. estándar muestral |
|---|---:|---:|
| Accuracy | 0.825845 | 0.013486 |
| Precision | 0.834689 | 0.041732 |
| Recall | 0.684983 | 0.061566 |
| F1-score | 0.749988 | 0.028931 |
| ROC-AUC | 0.862269 | 0.019814 |

La variabilidad es baja para accuracy y más alta para recall.

El recall varía aproximadamente entre:

```text
0.6111 y 0.7593
```

por lo que la estabilidad del modelo no se interpreta de forma uniforme para todas las métricas.

---

# 11. Consideración metodológica sobre el Hold-Out de la Sumativa

La partición Hold-Out de 179 observaciones ya fue utilizada durante Semana 3 en la comparación de arquitecturas.

Por este motivo, en Semana 4 se conserva como:

- evidencia histórica de desempeño;
- control de continuidad;
- referencia comparativa.

No se presenta como una muestra completamente independiente posterior a la selección del modelo.

La evidencia adicional de estabilidad se obtiene mediante validación cruzada sobre entrenamiento.

El conjunto test no se utiliza para:

- seleccionar arquitectura;
- ajustar hiperparámetros;
- estimar parámetros de preprocesamiento;
- optimizar el umbral.

---

# 12. Controles de la Evaluación Sumativa

La corrida archivada presenta:

```text
9/9 celdas de código ejecutadas secuencialmente
0 errores almacenados
0 ConvergenceWarning
50/50 artefactos requeridos presentes
```

También se verifica:

- continuidad de configuración con Semana 3;
- continuidad de predicciones;
- continuidad de métricas;
- integridad del dataset mediante SHA-256;
- consistencia entre métricas y matrices;
- ausencia de observaciones de test dentro del K-Fold.

La última celda informa:

```text
Control final de consistencia: OK
Continuidad con Semana 3: OK
Artefactos requeridos: OK
```

---

# 13. Evidencia de la Evaluación Sumativa

## Notebook

- [F4_Evaluacion.ipynb](notebook/F4_Evaluacion.ipynb)

## Informe

- [Informe final PDF · S4_2](informe/MCDI504_S4_2_GRUPO6.pdf)
- [Informe editable DOCX · S4_2](informe/MCDI504_S4_2_GRUPO6.docx)

## Documentación

- [Decisiones metodológicas](docs/DECISIONES_METODOLOGICAS.md)
- [Resultados y decisiones](docs/RESULTADOS_Y_DECISIONES.md)
- [Trazabilidad de la rúbrica](docs/TRAZABILIDAD_RUBRICA.md)
- [Auditoría final](docs/AUDITORIA_FINAL.md)
- [Fuentes base](docs/FUENTES_BASE.md)
- [Guía de ejecución](docs/GUIA_EJECUCION.md)
- [Manifiesto final de Semana 4](docs/MANIFIESTO_REPOSITORIO_FINAL.csv)

## Evidencia computacional

- [Datos](data/)
- [Outputs](outputs/)
- [Figuras](figures/)

---

# 14. Entorno reproducible

La raíz del repositorio contiene:

```text
requirements.txt
```

para documentar las dependencias del proyecto.

La ejecución archivada de Semana 4 registra como referencia:

- Python 3.12.4
- NumPy 1.26.4
- pandas 2.2.2
- scikit-learn 1.4.2
- Matplotlib 3.8.4

Desde la raíz del repositorio:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

---

# 15. Relación entre Formativa y Sumativa

La Evaluación Formativa y la Evaluación Sumativa responden a objetivos diferentes pero complementarios.

| Aspecto | Formativa 4 · S4_1 | Sumativa 3 · S4_2 |
|---|---|---|
| Propósito | Comparación preliminar y validación | Evaluación final del modelo seleccionado |
| Modelos Hold-Out | 7 modelos | MLP de 2 capas |
| Modelo sometido a CV | MLP de 1 capa | MLP de 2 capas |
| CV | Stratified K-Fold k=5 | Stratified K-Fold k=5 |
| Enfoque | Comparación y estabilidad | Validación final y trazabilidad |
| Informe | `MCDI504_S4_1_GRUPO6.pdf` | `MCDI504_S4_2_GRUPO6.pdf` |
| Ubicación | `Semana4/Formativa/` | `Semana4/` |

La Formativa permite estudiar comparativamente los modelos antes del cierre, mientras que la Sumativa profundiza sobre la arquitectura seleccionada para el cierre de la Fase 4.

---

# 16. Reproducibilidad y trazabilidad

La Semana 4 conserva evidencia suficiente para reconstruir el proceso analítico:

```text
dataset
   ↓
preprocesamiento
   ↓
partición Hold-Out
   ↓
entrenamiento
   ↓
predicciones
   ↓
matrices de confusión
   ↓
métricas
   ↓
validación cruzada
   ↓
estabilidad
   ↓
interpretación
   ↓
informe
```

Los notebooks, outputs, figuras, documentos metodológicos e informes se mantienen separados por evaluación para evitar mezclar evidencia formativa y sumativa.

---

# 17. Integridad del proyecto

La documentación de Semana 4 incorpora manifiestos de integridad para verificar rutas, tamaños y hashes de los archivos archivados.

Manifiesto Formativa:

```text
Formativa/docs/MANIFIESTO_FORMATIVA_FINAL.csv
```

Manifiesto general:

```text
docs/MANIFIESTO_REPOSITORIO_FINAL.csv
```

Estos archivos permiten comprobar correspondencia entre el estado documentado y los artefactos incorporados al repositorio.

---

# 18. Navegación rápida

## Evaluación Formativa 4

- [README](Formativa/README.md)
- [Notebook](Formativa/notebook/F4_Evaluacion.ipynb)
- [Informe PDF](Formativa/informe/MCDI504_S4_1_GRUPO6.pdf)
- [Informe DOCX](Formativa/informe/MCDI504_S4_1_GRUPO6.docx)
- [Outputs](Formativa/outputs/)
- [Figuras](Formativa/figures/)
- [Documentación](Formativa/docs/)

## Evaluación Sumativa 3

- [Notebook](notebook/F4_Evaluacion.ipynb)
- [Informe PDF](informe/MCDI504_S4_2_GRUPO6.pdf)
- [Informe DOCX](informe/MCDI504_S4_2_GRUPO6.docx)
- [Outputs](outputs/)
- [Figuras](figures/)
- [Documentación](docs/)

---

## Repositorio

Repositorio público del proyecto:

https://github.com/edocontreras/mcdi504-machine-learning-1
