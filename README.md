Descripción del Script de Preprocesamiento

Este script realiza el preprocesamiento completo del dataset relacionado con enfermedad cardiovascular. Su finalidad es limpiar, transformar y preparar los datos para su posterior uso en modelos de Machine Learning, garantizando que todas las variables estén correctamente tratadas y en un formato adecuado para entrenamiento.

Proceso de Preprocesamiento

Carga del dataset
El script monta Google Drive y carga el archivo CSV original. También contempla la posibilidad de que el archivo use diferentes delimitadores, asegurando una lectura correcta.

Separación de variables
Se separa la variable objetivo, que es la columna “cardio”, del resto de características predictoras.

Winsorización
Se aplica winsorización personalizada a todas las variables numéricas. Esto significa que los valores extremos se recortan ligeramente para disminuir el impacto de outliers, manteniendo la integridad general de los datos sin eliminar información.

Hard Clipping
Se utiliza un transformador propio llamado HardClipper. Este transformador limita los valores de ciertas variables numéricas a rangos definidos manualmente, basados en criterios fisiológicos razonables. Por ejemplo, se impone un mínimo y máximo esperado para la edad, peso, altura y valores de presión arterial, evitando datos imposibles o anómalos.

Definición de pipelines
Las variables se agrupan en tres tipos principales: numéricas, ordinales y binarias. Cada grupo recibe un tratamiento diferente:

Las variables numéricas se someten a recorte rígido, imputación de valores faltantes mediante la media, winsorización y estandarización.

Las variables ordinales se imputan según la categoría más frecuente y luego se codifican mediante OneHotEncoder.

Las variables binarias simplemente imputan valores faltantes utilizando el valor más frecuente.

Integración de todas las transformaciones
Con un ColumnTransformer, el script aplica cada pipeline al grupo de variables correspondiente. Esto produce un conjunto uniforme de datos transformados, donde todas las características están limpias, imputadas, normalizadas o codificadas según corresponda.

Generación del dataset final
Una vez transformadas todas las variables, se construye un nuevo DataFrame que contiene únicamente las características procesadas. A este conjunto final se le agrega nuevamente la columna “cardio” como variable objetivo. Posteriormente, el archivo resultante se guarda con el nombre dataset_preprocesado_completo.csv.

Exportación y descarga
El archivo preprocesado se almacena en Google Drive y luego se descarga automáticamente al entorno local del usuario.
