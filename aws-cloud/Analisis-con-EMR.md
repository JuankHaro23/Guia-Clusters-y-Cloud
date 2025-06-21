## Análisis Interactivo con Amazon EMR, Hue y Hive

[cite_start]**Amazon EMR (Elastic MapReduce)** es un servicio web gestionado de AWS que facilita el despliegue y la gestión de clústeres para el procesamiento de Big Data. [cite_start]EMR automatiza la instalación y configuración de frameworks como Hadoop, Spark y Hive.

### Ecosistema de Herramientas

* [cite_start]**Hue (Hadoop User Experience):** Es una interfaz de usuario web de código abierto que se integra con EMR para facilitar la interacción con el clúster. A través de Hue, se puede:
    * [cite_start]Navegar por el sistema de archivos HDFS con un explorador de archivos gráfico.
    * [cite_start]Subir datasets directamente desde el equipo local.
    * [cite_start]Ejecutar consultas interactivas y monitorizar trabajos.
    * [cite_start]Crear visualizaciones (gráficos de barras, mapas, etc.) a partir de los resultados.

* [cite_start]**Apache Hive:** Es una infraestructura de *data warehouse* construida sobre Hadoop. [cite_start]Su principal característica es que permite a los usuarios consultar grandes conjuntos de datos almacenados en HDFS utilizando **HiveQL**, un lenguaje de consulta muy similar a SQL. [cite_start]Cada consulta HiveQL se traduce de forma transparente en un trabajo MapReduce (o Tez) que se ejecuta en el clúster EMR.

### Flujo de Análisis de Datos con EMR y Hue

El proceso típico para analizar un conjunto de datos (ej. transacciones de compras) es el siguiente:

1.  [cite_start]**Lanzar un Clúster EMR:** Desde la consola de AWS, se crea un clúster seleccionando las aplicaciones deseadas (Hadoop, Hive, Hue) y configurando los nodos (tipo de instancia, número de nodos, etc.).
2.  [cite_start]**Ingesta de Datos:** A través de la interfaz de **Hue**, se sube el fichero de datos (ej. `purchases.txt`) al sistema de ficheros HDFS del clúster.
3.  **Creación de una Tabla Hive:** Se utiliza el asistente de Hue para crear una tabla a partir del fichero subido. [cite_start]Se define el formato (ej. CSV separado por tabuladores) y el esquema, es decir, el nombre y tipo de cada columna (`date`, `city`, `cost`, etc.).
4.  **Consulta con HiveQL:** En el editor de Hive de Hue, se escriben y ejecutan consultas SQL-like para analizar los datos. Por ejemplo, para obtener las transacciones de más de 100$ agrupadas por categoría:
    ```sql
    SELECT category, COUNT(*)
    FROM purchases
    WHERE cost > 100
    GROUP BY category;
    ```
5.  [cite_start]**Visualización:** Los resultados de la consulta se pueden visualizar directamente en Hue, creando gráficos de barras para ver las categorías más populares o, si se dispone de datos geográficos, se pueden cruzar con otra tabla de coordenadas de ciudades para **visualizar las transacciones en un mapa interactivo**.
