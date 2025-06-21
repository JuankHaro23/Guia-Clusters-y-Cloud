## Alta Disponibilidad (HA) y Balanceo de Carga

Para construir un servicio web robusto y escalable, se implementan mecanismos de alta disponibilidad y balanceo de carga en el front-end del clúster.

### Alta Disponibilidad (High Availability)

El objetivo es eliminar los puntos únicos de fallo. En nuestra arquitectura, el nodo maestro es un punto crítico, por lo que se duplica.

* **Arquitectura Activo-Pasivo:** Se utilizan dos nodos maestros, `master` (activo) y `standby` (pasivo).
* **IP Virtual:** Ambos nodos comparten una dirección IP virtual. Las peticiones de los clientes siempre se dirigen a esta IP.
* **Mecanismo de Failover:** El nodo `standby` monitoriza constantemente al nodo `master`. Si detecta una caída (ya sea del hardware o del servicio de balanceo), el nodo `standby` toma el control de la IP virtual y asume el rol de nodo activo, garantizando la continuidad del servicio.
* **Herramientas:** Este mecanismo se implementa con software como **Keepalived** o **Heartbeat**.

### Balanceo de Carga (Load Balancing)

El nodo maestro activo se encarga de distribuir las peticiones HTTP entrantes de manera equitativa entre los diferentes servidores web del back-end.

* **Distribución de Carga:** Reparte el trabajo para evitar que un solo servidor se sobrecargue y para permitir que el rendimiento del sistema escale horizontalmente al añadir más servidores.
* **Herramientas:** La distribución de carga se implementa usando una combinación de:
    * **LVS (Linux Virtual Server):** Un balanceador de carga de alto rendimiento que opera a nivel de kernel (Capa 4), lo que lo hace muy rápido.
    * **HAProxy:** Un balanceador de carga y proxy inverso muy popular y flexible, que puede operar a Capa 4 y Capa 7, permitiendo tomar decisiones de enrutamiento basadas en el contenido de las peticiones HTTP.
