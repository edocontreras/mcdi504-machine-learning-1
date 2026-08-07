# Datos utilizados

`iris_original.csv` corresponde a la representación del dataset Iris cargada directamente por `sklearn.datasets.load_iris()` en `Semana1/notebook/F1_Definicion.ipynb`. No se utiliza una descarga externa ni una edición manual del archivo para el análisis.

La exportación contiene 150 observaciones, cuatro predictores morfológicos continuos medidos en centímetros (`Sepal.Length`, `Sepal.Width`, `Petal.Length`, `Petal.Width`) y la variable objetivo categórica nominal `Species` (`setosa`, `versicolor`, `virginica`).

La secuencia de trazabilidad es:

`load_iris()` → `DataFrame bbdd1` → `Semana1/data/iris_original.csv` → análisis y archivos derivados.
