## Instalación y Clonación de Nodos (PXE)

La instalación de los nodos servidores se realiza de forma centralizada y escalable desde el nodo `Master`, evitando la necesidad de instalar cada máquina individualmente.

### Flujo de Instalación

1.  **Creación del Nodo "Modelo":**
    * Se clona la máquina `Base` para crear una nueva VM llamada `Modelo`.
    * Esta VM se configura tal y como queremos que queden los servidores finales: la red se configura por DHCP, se ajusta el `/etc/fstab` para usar los nombres de dispositivo (`/dev/sda1`) en lugar de UUIDs, y se instala y configura el cargador de arranque GRUB.

2.  **Copia del Modelo al Servidor NFS:**
    * Una vez que el nodo `Modelo` está listo, su sistema de archivos completo se copia al servidor `NFS` usando `rsync`. Esta imagen del sistema se almacena en una ruta específica (ej. `/data/srv/images/model`) y servirá como la fuente para todos los nodos servidores.

3.  **Arranque por Red (PXE):**
    * Los nodos `Server1`, `Server2`, etc., se inician sin un sistema operativo local. Se configuran para arrancar desde la red (PXE) como primera opción.
    * El servidor **DHCP/PXE** en el nodo `Master` les asigna una dirección IP y les proporciona el cargador de arranque, el kernel y un ramdisk inicial.
    * Crucialmente, el sistema de archivos raíz que montan estos nodos al arrancar es una **imagen temporal compartida que reside en el servidor NFS**.

4.  **Clonación desde el Master:**
    * Con todos los servidores arrancados en este modo temporal, el nodo `Master` lanza comandos remotos (`ssh`, `psh`, `cssh`) a todos ellos simultáneamente para:
        * **Particionar el disco duro local** de cada servidor usando `sfdisk` con una plantilla guardada del nodo `Modelo`.
        * **Formatear las particiones** (`mkfs.ext4`).
        * **Montar la partición local** en un punto temporal (ej. `/run/sda1`).
        * **Copiar la imagen del sistema** desde el NFS al disco local recién montado (`cp -ax /images/model/* /run/sda1`).
        * **Instalar GRUB** en el MBR del disco duro local de cada servidor.

5.  **Reinicio Final:**
    * Se modifica la configuración del servidor PXE en el `Master` para que la opción por defecto sea arrancar desde el disco local (`localboot`).
    * Se lanza una orden de reinicio a todos los servidores. Al arrancar, ahora lo harán desde su disco local, ya con el sistema completamente instalado y configurado.
