# Auditoría final de la corrida y del repositorio

## Notebook

- Nombre: `F4_Evaluacion.ipynb`.
- Celdas de código: 9.
- Celdas ejecutadas: 9/9.
- Secuencia de ejecución: 1 a 9.
- Errores almacenados: 0.
- Mensajes finales: `Control final de consistencia: OK`, `Continuidad con Semana 3: OK`, `Artefactos requeridos: OK`.

## Consistencia numérica

- Las métricas Hold-Out fueron recalculadas desde `24_predicciones_holdout.csv` y coinciden con `22_metricas_holdout.csv`.
- Matriz Hold-Out: TN=92, FP=18, FN=19, TP=50; suma 179.
- Las estadísticas de estabilidad fueron recalculadas desde los cinco folds y coinciden con `15_resumen_estabilidad_cv.csv`.
- La matriz OOF agregada suma 712 observaciones y cada índice de entrenamiento aparece exactamente una vez.
- El manifiesto SHA-256 generado por el notebook coincide con los archivos de la corrida.
- `40_control_artefactos_requeridos.csv` registra 50/50 artefactos presentes.
- `26_reporte_clasificacion_holdout.csv` conserva únicamente filas con soporte estadístico definido; accuracy global se reporta en `22_metricas_holdout.csv`.

## Resultados principales

- Hold-Out: accuracy=0.793296, precision=0.735294, recall=0.724638, F1=0.729927, ROC-AUC=0.852174.
- CV 5 folds: accuracy promedio=0.825845 (SD muestral=0.013486); recall promedio=0.684983 (SD muestral=0.061566).
- K-Fold externo: 5 ajustes; LOOCV teórico: 712 ajustes.

## Metodología

- `Pipeline` reajustado dentro de cada fold.
- `StratifiedKFold(k=5)` aplicado solo a entrenamiento.
- Umbral 0.50 no optimizado con test.
- Se declara que el Hold-Out ya fue utilizado para comparación arquitectónica en Semana 3; por tanto, su papel en Semana 4 es histórico y de continuidad.

## Figuras

- 8 figuras PNG generadas y revisadas contra sus tablas fuente.
- No se detectaron discrepancias entre cifras visualizadas y outputs tabulados.

## Limpieza GitHub

- `.ipynb_checkpoints` eliminado.
- `.gitkeep` eliminado de carpetas pobladas.
- Sin archivos temporales de Office, `.DS_Store`, `Thumbs.db`, `*.pyc`, `*.tmp` o `*.bak` en el repositorio final.
- `.gitignore` actualizado para prevenir artefactos locales comunes.

## Dependencias

- `requirements.txt` fue contrastado con los imports de los notebooks de Semanas 1-4.
- Dependencias externas cubiertas: NumPy, pandas, Matplotlib, scikit-learn, seaborn, SciPy, Jupyter Notebook e ipykernel.
- La corrida de Semana 4 registra Python 3.12.4, NumPy 1.26.4, pandas 2.2.2, scikit-learn 1.4.2 y Matplotlib 3.8.4, coherentes con las versiones fijadas en el proyecto para los componentes críticos.

## Informe

- `MCDI504_S4_2_GRUPO6.docx`.
- `MCDI504_S4_2_GRUPO6.pdf`.
- 23 páginas.
- Formato institucional conservado a partir del entregable oficial.
- Cuerpo principal en Calibri 11, tamaño carta y jerarquía de títulos institucional.
- Índice con numeración de páginas verificada.
- 8 figuras incorporadas desde la corrida archivada.
- Referencias: 2 fuentes docentes, 3 fuentes técnicas oficiales y 2 académicas complementarias; correspondencia cita-referencia verificada y referencias normalizadas con sangría francesa.
- Revisión visual completa de las 23 páginas: sin cortes, solapamientos, glifos defectuosos ni páginas vacías.
- Auditoría de accesibilidad DOCX: 0 hallazgos de severidad alta; se conserva un hallazgo medio por la tabla de índice sin fila de encabezado semántica, que no afecta la presentación.
- Documento sin comentarios de revisión; no se detectaron cambios controlados activos.
- Preflight PDF: 23 páginas, no cifrado, abrible y no escaneado.

## Alineación con la evaluación

- La trazabilidad C1-C17 está documentada en `TRAZABILIDAD_RUBRICA.md` y en el Anexo C del informe.
- Se cubren matriz de confusión, accuracy, precision, recall, F1-score, ROC-AUC, Precision-Recall, umbral, Hold-Out, K-Fold, referencia de costo LOOCV y prevención de data leakage.
- La justificación de validación relaciona explícitamente tamaño del conjunto de datos, costo computacional y estabilidad de métricas.
- El informe, notebook, outputs, figuras y documentación utilizan una única corrida archivada y una nomenclatura consistente.

## Manifiesto del repositorio

El archivo `MANIFIESTO_REPOSITORIO_FINAL.csv` se genera al cierre del proceso y registra ruta, tamaño y SHA-256 de todos los archivos del snapshot final, excluyéndose a sí mismo para evitar autorreferencia.
