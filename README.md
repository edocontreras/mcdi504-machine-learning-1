# MCDI504 · Machine Learning I
## Fase 1 · Definición y orientación de la situación

**Proyecto:** IrisFlow  
**Docente:** Dr. David Ruete Zúñiga  
**Grupo:** 6  
**Integrantes:** Luis Díaz Giral · Gonzalo Bouldres · Eduardo Contreras  
**Fecha de entrega:** 08-08-2026

## Propósito

El repositorio documenta la Fase 1 del proyecto ABP mediante una única cadena de evidencia: definición analítica del problema, notebook ejecutado, datos utilizados, resultados exportados, figuras, decisiones técnicas e informe final. El alcance corresponde a definición del problema, caracterización inicial de datos, selección del tipo de aprendizaje y articulación con KDD; no se ejecuta entrenamiento de modelos ni evaluación predictiva.

## Estructura

```text
mcdi504-machine-learning-1/
├── README.md
├── requirements.txt
├── .gitignore
└── Semana1/
    ├── data/
    │   ├── README.md
    │   └── iris_original.csv
    ├── docs/
    │   ├── DECISIONES_TECNICAS.md
    │   ├── FUENTES.md
    │   └── TRAZABILIDAD.md
    ├── figures/
    │   ├── boxplot_variables.png
    │   ├── correlacion_pearson.png
    │   ├── distribucion_species.png
    │   ├── flujo_kdd.png
    │   └── pvalores_pearson.png
    ├── informe/
    │   └── MCDI504_S1_1_GRUPO6.pdf
    ├── notebook/
    │   └── F1_Definicion.ipynb
    └── outputs/
        └── 14 archivos CSV
```

## Notebook y evidencia computacional

`Semana1/notebook/F1_Definicion.ipynb` conserva la ejecución completa realizada para la entrega: 22 celdas de código con conteos de ejecución consecutivos del 1 al 22 y sin salidas de error almacenadas. La última celda registra el inventario de la evidencia generada por la misma ejecución.

La ejecución exporta `iris_original.csv`, 14 archivos CSV y 5 figuras PNG. Los principales resultados son:

- 150 observaciones y 5 variables; 0 valores faltantes y 3 clases de `Species`.
- 50 observaciones por clase, equivalentes a 33,33 % por categoría.
- Dos registros con combinación completa coincidente en los índices 101 y 142; `duplicated().sum()` contabiliza una repetición respecto de una fila previa.
- Cuatro valores atípicos relativos por Tukey en `Sepal.Width`; no se eliminan automáticamente.
- La mayor correlación entre predictores corresponde a `Petal.Length`–`Petal.Width` (`r ≈ 0,963`).
- Para `Sepal.Length`–`Sepal.Width`, `p ≈ 0,152`; con `α = 0,05` no se rechaza `H0: ρ = 0`.
- La transformación Min-Max se aplica solo a predictores y produce mínimo 0 y máximo 1 en cada variable transformada.

## Trazabilidad

La correspondencia entre rúbrica, informe, notebook y archivos exportados se encuentra en [`Semana1/docs/TRAZABILIDAD.md`](Semana1/docs/TRAZABILIDAD.md). Las decisiones y ajustes metodológicos están documentados en [`Semana1/docs/DECISIONES_TECNICAS.md`](Semana1/docs/DECISIONES_TECNICAS.md), y el control de fuentes se mantiene en [`Semana1/docs/FUENTES.md`](Semana1/docs/FUENTES.md).

El informe formal se encuentra en [`Semana1/informe/MCDI504_S1_1_GRUPO6.pdf`](Semana1/informe/MCDI504_S1_1_GRUPO6.pdf).

## Reproducibilidad

Crear un entorno virtual e instalar las dependencias fijadas en `requirements.txt`:

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook
```

Abrir `Semana1/notebook/F1_Definicion.ipynb`. Una reproducción desde cero puede realizarse mediante **Restart Kernel and Run All Cells**; la ejecución reemplaza los archivos derivados en `Semana1/outputs/`, `Semana1/figures/` y `Semana1/data/iris_original.csv`.
