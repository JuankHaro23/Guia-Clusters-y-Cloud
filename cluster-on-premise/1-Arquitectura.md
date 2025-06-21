## Arquitectura del Clúster Web de Alta Disponibilidad

El objetivo de este proyecto es construir un servidor web tolerante a fallos y con distribución de carga. La arquitectura se basa en un clúster de 6 nodos virtualizados con VirtualBox.

### Componentes Clave:
* **Front-end (Nodos Maestros):** Dos nodos (`master` y `standby`) en configuración activo-pasivo para garantizar alta disponibilidad. Estos nodos gestionan la IP virtual pública y distribuyen las peticiones HTTP entrantes. Se utiliza **Keepalived** para la gestión de la alta disponibilidad y **LVS/HAProxy** para el balanceo de carga.
* **Back-end (Servidores Web):** Tres servidores reales (`server1`, `server2`, `server3`) que ejecutan Apache para atender las peticiones HTTP. La comunicación con el front-end se realiza a través de una red interna.
* **Almacenamiento Centralizado:** Un servidor NFS que almacena las páginas web, asegurando que todos los servidores del back-end sirvan el mismo contenido. Este nodo también implementa un **RAID por software** para la redundancia de datos.
* **Redes:** Se usan dos redes virtuales: una **Red Externa** (nat-network en VirtualBox) para el acceso desde Internet y una **Red Interna** (internal network) para la comunicación entre los nodos del clúster.
