## Análisis de Big Data con Hadoop y MapReduce

[cite_start]**Apache Hadoop** es el framework de código abierto de referencia para el almacenamiento y procesamiento distribuido de grandes conjuntos de datos (Big Data).

### Paradigma MapReduce

[cite_start]Es un modelo de programación que divide una tarea de procesamiento masivo en dos fases principales:

1.  **Fase Map:** El conjunto de datos de entrada se divide en fragmentos, y cada fragmento es procesado de forma paralela por una tarea "Mapper". [cite_start]Esta fase se encarga de filtrar y transformar los datos, emitiendo pares clave-valor intermedios. [cite_start]Por ejemplo, en un problema de conteo de palabras, un mapper lee un bloque de texto y emite un par `(palabra, 1)` por cada palabra que encuentra.

2.  **Fase Reduce:** Los pares intermedios generados en la fase Map se agrupan por clave y se procesan por tareas "Reducer". [cite_start]Esta fase se encarga de agregar los datos para obtener el resultado final. [cite_start]Siguiendo el ejemplo, un reducer recibe una palabra y una lista de "1s", y su trabajo es sumarlos para obtener la frecuencia total de esa palabra.

### Componentes del Ecosistema

* [cite_start]**HDFS (Hadoop Distributed File System):** Es el sistema de archivos de Hadoop, diseñado para ser tolerante a fallos y almacenar datos de gran tamaño a través de un clúster de máquinas. [cite_start]La interacción se realiza mediante la línea de comandos (`hadoop fs -ls`, `hadoop fs -put`, etc.).

* [cite_start]**Hadoop Streaming:** Una potente utilidad que permite usar cualquier script o ejecutable (en **Python**, Ruby, Bash, etc.) como mapper o reducer. [cite_start]El único requisito es que el script lea datos de la entrada estándar y escriba los resultados en la salida estándar, lo que agiliza enormemente el ciclo de desarrollo al no depender exclusivamente de Java.

### Flujo de trabajo práctico

1.  **Preparar los scripts** de `mapper.py` y `reducer.py`.
2.  **Probar localmente** los scripts con una pequeña porción de los datos para depurar errores rápidamente.
    ```bash
    cat /datos/locales.txt | ./mapper.py | sort -k1,1 | ./reducer.py
    ```
3.  **Subir el dataset** a HDFS (`hadoop fs -put`).
4.  **Lanzar el trabajo** en el clúster Hadoop usando Hadoop Streaming, especificando los scripts, el directorio de entrada en HDFS y el directorio de salida.
