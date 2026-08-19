# Auditoría final de la corrida y del repositorio

## Notebook

- Nombre: `F3_RedesNeuronales.ipynb`
- Celdas totales: 31
- Celdas de código: 15
- Celdas ejecutadas: 15/15
- Secuencia de ejecución: 1 a 15
- Errores: 0
- Mensaje final: `Validación de artefactos: OK`

## Consistencia numérica

- Las métricas de regresión fueron recalculadas desde `11_reg_predicciones_test.csv` y coinciden con `10_reg_metricas_comparacion.csv`.
- Las tres matrices de confusión suman 179 observaciones cada una.
- Accuracy, precision, recall, F1, balanced accuracy, especificidad, TN, FP, FN y TP coinciden exactamente entre las predicciones y `23_clf_metricas_mlp.csv`.
- El control de preprocesamiento informa 0 NaN en train y 0 NaN en test.
- `25_clf_advertencias_mlp.csv` no registra advertencias.

## Regresión

- 20.640 observaciones.
- 8 predictores.
- Objetivo: `MedHouseVal`.
- 0 valores faltantes.
- Split 80/20.
- GridSearchCV: 72 configuraciones y 5 folds, exclusivamente sobre entrenamiento.
- Mejor configuración del árbol: {'max_depth': 12, 'min_samples_leaf': 10, 'min_samples_split': 2}.
- Modelo con mejor desempeño de prueba: MLPRegressor, RMSE=0.549301, R²=0.769742.

## Clasificación

- 891 observaciones.
- Objetivo: `survived`.
- Split estratificado 712/179.
- 8 predictores después de transformación.
- Arquitecturas: `(100,)`, `(100, 50)`, `(100, 50, 25)`.
- Arquitectura con mejor desempeño global equilibrado: MLP 2 capas ocultas.
- No se detectaron errores de ejecución ni faltantes en artefactos obligatorios.

## Figuras

- 15 figuras PNG.
- Las figuras fueron revisadas visualmente: distribución, tuning, comparación de regresión, EDA, tres matrices de confusión, curvas de entrenamiento/validación, métricas y complejidad.

## Informe

- `f3_s03_grupo6.docx`
- `f3_s03_grupo6.pdf`
- 23 páginas.
- Índice con páginas.
- Revisión visual completa: sin cortes, solapamientos ni páginas vacías.

## Limpieza GitHub

- `.ipynb_checkpoints` eliminado.
- `.gitkeep` eliminado de carpetas pobladas.
- Sin archivos temporales de Office.
- Documentación actualizada al estado post-ejecución.
