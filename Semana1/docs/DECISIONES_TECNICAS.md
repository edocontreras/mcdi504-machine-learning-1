# Decisiones técnicas · Fase 1

## 1. Variable objetivo y tipo de aprendizaje

`Species` se mantiene como variable categórica nominal. La etiqueta está disponible para las 150 observaciones y contiene tres categorías; por ello, el problema se formula como **aprendizaje supervisado de clasificación multiclase**.

Evidencia: sección 2 del notebook y `Semana1/outputs/comparacion_enfoques.csv`.

## 2. Control de integridad

La ejecución registra 150 observaciones, 5 variables, 0 valores faltantes y 3 clases de `Species`. La distribución es de 50 observaciones por clase.

Los índices 101 y 142 presentan valores idénticos en los cuatro predictores y en `Species`. `duplicated().sum()` contabiliza una repetición respecto de una fila previa, pero la información disponible no permite establecer si corresponde a una misma unidad experimental o a observaciones distintas con mediciones coincidentes. Ambos registros se conservan en Fase 1.

Evidencia: `Semana1/outputs/control_integridad.csv`, `Semana1/outputs/registros_coincidentes.csv`, `Semana1/outputs/distribucion_clases.csv` y sección 5 del notebook.

## 3. Valores atípicos

El criterio de Tukey (`1,5 × IQR`) identifica cuatro valores atípicos relativos en `Sepal.Width` y ninguno en los otros tres predictores. No se aplica eliminación automática, porque la condición de atípico estadístico no constituye evidencia suficiente de error de medición.

Evidencia: `Semana1/outputs/atipicos_tukey.csv`, `Semana1/figures/boxplot_variables.png` y sección 6 del notebook.

## 4. Codificación temporal de `Species`

Se genera una copia donde las categorías de `Species` reciben identificadores numéricos temporales 1, 2 y 3. La codificación se utiliza únicamente como apoyo exploratorio; no se interpreta como escala ordinal ni como variable continua.

Evidencia: `Semana1/outputs/codificacion_species.csv` y sección 7 del notebook.

## 5. Correlación de Pearson y valores p

La correlación de Pearson con interpretación inferencial se restringe a los cuatro predictores continuos. La asociación con `Species` codificada se conserva únicamente como evidencia exploratoria.

La mayor correlación entre predictores es `Petal.Length`–`Petal.Width`, con `r ≈ 0,963`. Para `Sepal.Length`–`Sepal.Width`, `p ≈ 0,152`, por lo que no se rechaza `H0: ρ = 0` con `α = 0,05`. Los valores p no se emplean como criterio automático de selección de variables.

Evidencia: `Semana1/outputs/correlacion_predictores.csv`, `Semana1/outputs/correlacion_species_exploratoria.csv`, `Semana1/outputs/pvalores_predictores.csv` y secciones 8–9 del notebook.

## 6. Normalización

Min-Max se aplica exclusivamente a los predictores y `Species` conserva su naturaleza categórica. La verificación exportada registra mínimo 0 y máximo 1 para cada predictor transformado.

Evidencia: `Semana1/outputs/iris_normalizado.csv`, `Semana1/outputs/verificacion_normalizacion.csv` y sección 10 del notebook.

## 7. Alcance metodológico

Fase 1 no ejecuta partición entrenamiento/prueba, entrenamiento de estimadores, ajuste de hiperparámetros ni métricas predictivas. La decisión responde al alcance explícito de la actividad y mantiene el modelamiento como etapa de KDD no ejecutada en este avance.

## 8. Ajustes metodológicos registrados

Durante la consolidación de Fase 1 se registraron tres ajustes metodológicos:

1. Las observaciones de índices 101 y 142 se documentan como **registros con combinación de valores coincidente**, sin afirmar duplicación de una misma unidad experimental.
2. La inferencia de Pearson se restringe a predictores continuos; la codificación de `Species` queda limitada a apoyo exploratorio.
3. La normalización Min-Max se aplica únicamente a predictores y mantiene `Species` fuera de la transformación.

**Decisión de alcance.** Fase 1 excluye partición entrenamiento/prueba, entrenamiento de modelos, ajuste de hiperparámetros y métricas predictivas, en correspondencia con las instrucciones de la actividad.

Los tres ajustes y la decisión de alcance mantienen coherencia entre la naturaleza de los datos, el enfoque supervisado multiclase, el notebook, los archivos exportados y el informe.
