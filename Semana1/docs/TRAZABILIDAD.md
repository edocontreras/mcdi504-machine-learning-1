# Trazabilidad de Fase 1

La cadena de evidencia del proyecto es:

**problema y decisiones metodológicas → notebook ejecutado → datos/resultados/figuras → informe final**.

## Correspondencia con la rúbrica

| Criterio | Informe | Notebook | Evidencia principal |
|---|---|---|---|
| C1 · Introducción y contextualización | II | 1 | `README.md` |
| C2 · Problemática y objetivos | III | 1 | `Semana1/notebook/F1_Definicion.ipynb` |
| C3 · Clasificación del tipo de aprendizaje | IV | 2 | `Semana1/docs/DECISIONES_TECNICAS.md` |
| C4 · Machine Learning y KDD | V | 3 | `Semana1/figures/flujo_kdd.png`, `Semana1/outputs/kdd_aplicado.csv` |
| C5 · Notebook F1_Definición | VI | 1–13 | `Semana1/notebook/F1_Definicion.ipynb` |
| C6 · Comparación de enfoques | VII | 11 | `Semana1/outputs/comparacion_enfoques.csv` |
| C7 · Documentación del proceso | VIII | 5–11 | `Semana1/docs/DECISIONES_TECNICAS.md`, `Semana1/docs/TRAZABILIDAD.md` |
| C8 · Conclusiones | IX | — | `Semana1/informe/MCDI504_S1_1_GRUPO6.pdf` |
| C9 · Portada e índice | I | — | `Semana1/informe/MCDI504_S1_1_GRUPO6.pdf` |
| C10 · Formato institucional | documento completo | — | `Semana1/informe/MCDI504_S1_1_GRUPO6.pdf` |
| C11 · Ortografía y gramática | documento completo | — | `Semana1/informe/MCDI504_S1_1_GRUPO6.pdf` |
| C12 · Fuentes, citas y referencias | X | 12 | `Semana1/docs/FUENTES.md`, informe final |
| C13 · Anexos | XI | 4–13 | `Semana1/outputs/`, `Semana1/figures/`, informe final |

## Evidencias analíticas específicas

| Evidencia | Notebook | Archivo trazable |
|---|---|---|
| Dataset utilizado | 4 | `Semana1/data/iris_original.csv` |
| Estructura de variables | 4–5 | `Semana1/outputs/estructura_variables.csv` |
| Control de integridad | 5 | `Semana1/outputs/control_integridad.csv` |
| Registros coincidentes | 5 | `Semana1/outputs/registros_coincidentes.csv` |
| Distribución de clases | 5 | `Semana1/outputs/distribucion_clases.csv`, `Semana1/figures/distribucion_species.png` |
| Estadística descriptiva | 6 | `Semana1/outputs/resumen_descriptivo.csv` |
| Revisión de atípicos | 6 | `Semana1/outputs/atipicos_tukey.csv`, `Semana1/figures/boxplot_variables.png` |
| Codificación temporal de `Species` | 7 | `Semana1/outputs/codificacion_species.csv` |
| Correlación entre predictores | 8 | `Semana1/outputs/correlacion_predictores.csv`, `Semana1/figures/correlacion_pearson.png` |
| Exploración con `Species` codificada | 8 | `Semana1/outputs/correlacion_species_exploratoria.csv` |
| Valores p de Pearson | 9 | `Semana1/outputs/pvalores_predictores.csv`, `Semana1/figures/pvalores_pearson.png` |
| Normalización Min-Max | 10 | `Semana1/outputs/iris_normalizado.csv`, `Semana1/outputs/verificacion_normalizacion.csv` |
| Aplicación de KDD | 3 | `Semana1/outputs/kdd_aplicado.csv`, `Semana1/figures/flujo_kdd.png` |
| Comparación de enfoques | 11 | `Semana1/outputs/comparacion_enfoques.csv` |
| Inventario de evidencia generada | 13 | salida almacenada en `Semana1/notebook/F1_Definicion.ipynb` |

## Reglas de coherencia

- Los índices 101 y 142 se describen como registros con combinación de valores coincidente; no se afirma que correspondan necesariamente a la misma unidad experimental.
- Los valores atípicos se documentan sin eliminación automática.
- `Species` codificada no se interpreta como una variable cuantitativa natural.
- La inferencia de Pearson se restringe a predictores continuos.
- La normalización Min-Max se aplica únicamente a predictores.
- Fase 1 no incorpora entrenamiento, métricas predictivas ni modelamiento ejecutado.
- Los valores incluidos en el informe corresponden a los archivos generados por la ejecución almacenada en el notebook.
