## Despliegue de Clústeres HPC con AWS ParallelCluster

[cite_start]AWS ParallelCluster es una herramienta oficial de AWS que simplifica el despliegue y la gestión de clústeres para **Computación de Altas Prestaciones (HPC)**.

### Funcionamiento:
* **Elasticidad:** La herramienta despliega inicialmente solo el nodo principal. [cite_start]Los nodos de cómputo se crean y eliminan dinámicamente (de forma elástica) según la carga de trabajos en la cola. Esto optimiza los costes enormemente.
* [cite_start]**Gestor de Colas:** Se integra con gestores de colas estándar como **SLURM**.
* [cite_start]**Casos de Uso:** Ideal para ejecutar aplicaciones paralelas que usan MPI (Message Passing Interface).
* [cite_start]**Visualización Remota:** Permite la conexión gráfica al clúster mediante el protocolo **NICE DCV** para visualización científica (ej. con la herramienta Vedo).
