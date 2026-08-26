# Datos de la Formativa 4

La ejecución reutiliza como fuente canónica `Semana3/data/titanic.csv`. No se mantiene una segunda copia dentro de esta carpeta para evitar divergencias entre datasets.

El notebook verifica la identidad del archivo mediante SHA-256 y registra el hash en `outputs/01_perfil_dataset.csv`.

Variable objetivo: `survived` (0 = no sobrevivió; 1 = sobrevivió). Predictores: `pclass`, `age`, `sibsp`, `parch`, `fare`, `sex` y `embarked`.
