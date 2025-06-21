## Análisis Interactivo con Amazon EMR, Hue y Hive

[cite_start]**Amazon EMR (Elastic MapReduce)** es un servicio gestionado de AWS que facilita el despliegue de clústeres Hadoop, Spark y otras herramientas de Big Data.

### Herramientas del Ecosistema:
* **Hue (Hadoop User Experience):** Una interfaz web gráfica para interactuar con el clúster. [cite_start]Permite subir datos, ejecutar consultas y visualizar resultados de forma sencilla.
* **Hive:** Un sistema de *data warehouse* que se ejecuta sobre Hadoop. [cite_start]Permite realizar consultas sobre grandes datasets almacenados en HDFS usando un lenguaje muy similar a SQL llamado **HiveQL**. [cite_start]Cada consulta de Hive se traduce internamente a un trabajo MapReduce.
* [cite_start]**Visualización:** Hue permite crear visualizaciones interactivas directamente desde los resultados de las consultas, incluyendo gráficos de barras y mapas geográficos combinando diferentes datasets.
