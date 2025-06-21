## Configuración del Entorno Virtual con VirtualBox

[cite_start]La base del clúster on-premise se implementa sobre máquinas virtuales en VirtualBox.

1.  [cite_start]**Creación de la VM Base:** Se crea una máquina virtual inicial llamada `Base` con Debian "bullseye". [cite_start]Esta VM sirve como plantilla para evitar instalaciones repetitivas.
2.  **Configuración de Nodos:**
    * [cite_start]**Master/Standby:** 1 GB RAM, 10 GB disco, y dos interfaces de red (una a la Red NAT externa, otra a la red interna).
    * [cite_start]**Servidores Web y NFS:** 1 GB RAM, 10 GB disco, y una interfaz de red a la red interna.
3.  [cite_start]**Clonación:** Las máquinas `Master`, `NFS` y `Modelo` (para los servidores web) se generan clonando la VM `Base`, lo que agiliza enormemente el despliegue.
