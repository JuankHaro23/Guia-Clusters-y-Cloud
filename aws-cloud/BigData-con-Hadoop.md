## Análisis de Big Data con Hadoop y MapReduce

[cite_start]**Apache Hadoop** es el framework de código abierto por excelencia para el procesamiento distribuido de grandes volúmenes de datos.

### Componentes y Flujo de Trabajo:
* [cite_start]**HDFS (Hadoop Distributed File System):** Un sistema de ficheros distribuido sobre el que se ejecutan las aplicaciones. [cite_start]Se interactúa con él mediante comandos como `hadoop fs -ls`, `hadoop fs -put`, etc..
* **MapReduce:** Es el modelo de programación que divide el problema en dos fases:
    1.  [cite_start]**Fase Map:** Procesa los datos de entrada de forma paralela.
    2.  [cite_start]**Fase Reduce:** Agrega los resultados intermedios para obtener el resultado final.
* [cite_start]**Hadoop Streaming:** Una utilidad que permite escribir programas MapReduce en cualquier lenguaje (como Python), leyendo de la entrada estándar y escribiendo en la salida estándar, lo que simplifica enormemente el desarrollo.
