## Clústeres HPC con AWS ParallelCluster

[cite_start]**AWS ParallelCluster** es una herramienta de código abierto mantenida por AWS que simplifica y automatiza el despliegue y la gestión de clústeres para **Computación de Altas Prestaciones (HPC)** sobre la infraestructura de Amazon EC2.

### Características Principales

* [cite_start]**Despliegue Automatizado:** Utiliza un simple archivo de configuración para definir toda la arquitectura del clúster, incluyendo los tipos de instancia, la configuración de red, el gestor de colas y el almacenamiento compartido.
* **Elasticidad y Optimización de Costes:** Es su ventaja más significativa. El clúster no se crea con un tamaño fijo. [cite_start]Inicialmente, solo se despliega el **nodo principal (Head Node)**. [cite_start]Los **nodos de cómputo** se crean y se destruyen automáticamente en función del número de trabajos en la cola. [cite_start]Si no hay trabajos, los nodos de cómputo se terminan para no incurrir en costes innecesarios.
* [cite_start]**Gestor de Colas:** Se integra de forma nativa con gestores de trabajos estándar en el mundo HPC, como **SLURM**. [cite_start]Los usuarios interactúan con el clúster enviando trabajos a la cola de SLURM (`sbatch`).
* [cite_start]**Almacenamiento Compartido:** Configura automáticamente un sistema de archivos de red (NFS) para compartir directorios como `/home` entre el nodo principal y todos los nodos de cómputo. [cite_start]Esto garantiza que los ejecutables, scripts y datos estén disponibles para todos los nodos del clúster de manera transparente.

### Caso de Uso: Ejecución de Trabajos MPI

[cite_start]AWS ParallelCluster es ideal para ejecutar aplicaciones paralelas basadas en **MPI (Message Passing Interface)**, un estándar para la comunicación entre procesos en sistemas de memoria distribuida.

1.  [cite_start]**Conexión:** El usuario se conecta por SSH al nodo principal del clúster.
2.  [cite_start]**Compilación:** Se compila el código MPI (ej. `hello-mpi.c`) en el nodo principal usando `mpicc`.
3.  [cite_start]**Envío del Trabajo:** Se crea un script de envío (`.sh`) que invoca el ejecutable con `mpirun` y se envía al gestor de colas SLURM con el comando `sbatch`.
4.  **Escalado Automático:** Si no hay nodos de cómputo disponibles, ParallelCluster los aprovisiona automáticamente para ejecutar el trabajo. Una vez finalizado y tras un período de inactividad, los nodos se terminan.
5.  [cite_start]**Visualización:** Permite la conexión gráfica mediante el protocolo **NICE DCV** para visualizar resultados de forma remota, ideal para post-procesamiento de simulaciones científicas.
