# Resultados y decisiones de la corrida

## Desempeño Hold-Out histórico

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

Matriz de confusión: TN=92, FP=18, FN=19, TP=50.

La clase positiva presenta recall de 0.7246; por tanto, 27.54% de los positivos reales del Hold-Out se clasifican como negativos. La especificidad es 0.8364. Sin una función de costos explícita, no se interpreta uno de estos errores como universalmente más grave; su relevancia depende del objetivo aplicado.

## Validación cruzada estratificada

| Métrica | Promedio | Desv. estándar muestral | Mínimo | Máximo |
|---|---:|---:|---:|---:|
| Accuracy | 0.825845 | 0.013486 | 0.809859 | 0.845070 |
| Precision | 0.834689 | 0.041732 | 0.773585 | 0.883721 |
| Recall | 0.684983 | 0.061566 | 0.611111 | 0.759259 |
| F1-score | 0.749988 | 0.028931 | 0.709677 | 0.775510 |
| ROC-AUC | 0.862269 | 0.019814 | 0.833884 | 0.886834 |

Accuracy presenta baja variabilidad entre folds. Recall es la métrica obligatoria más sensible a la composición de las particiones, con un rango de 0.1481. Esta diferencia debe conservarse en la interpretación del informe.

## Decisión técnica

Se mantiene el MLP `(100, 50)` como modelo del proyecto. Semana 4 no introduce una nueva selección; aporta evidencia de estabilidad y caracteriza el perfil de errores. El K-Fold estratificado es adecuado para el objetivo de esta fase porque utiliza repetidamente el conjunto de entrenamiento con costo moderado y conserva la proporción de clases en los folds.

## Mejoras futuras

- incorporar una partición final verdaderamente independiente o evaluación externa si se requiere una estimación posterior a la selección;
- utilizar validación anidada si en el futuro se reabre el ajuste de hiperparámetros;
- definir una función de costos antes de ajustar el umbral;
- considerar calibración probabilística y/o evaluación repetida estratificada si el objetivo aplicado exige probabilidades o mayor precisión en la estimación de variabilidad.
