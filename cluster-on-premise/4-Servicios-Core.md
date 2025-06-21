## Servicios Clave: NFS y Autenticación con NIS

Para que el clúster funcione como un sistema cohesivo, se implementan dos servicios fundamentales: un sistema de archivos compartido (NFS) y un sistema de autenticación centralizado (NIS).

### NFS (Network File System)

NFS permite que los nodos del clúster compartan directorios a través de la red, lo cual es esencial para tener un único punto de almacenamiento para las páginas web y los directorios `home` de los usuarios.

* **Servidor NFS (en el nodo `nas`):**
    * Se instala el paquete `nfs-kernel-server`.
    * El archivo `/etc/exports` se configura para "exportar" o compartir el directorio `/data` con todos los nodos de la red interna (`10.0.100.0/24`).
    * Se usan opciones clave como `rw` (lectura/escritura) y `no_root_squash` (permite al usuario root de los clientes tener privilegios de root en el recurso compartido).

* **Clientes NFS (en `Master` y `Servers`):**
    * Se instala el paquete `nfs-common`.
    * El archivo `/etc/fstab` se modifica para montar automáticamente los directorios compartidos por el servidor NFS durante el arranque.

### NIS (Network Information Service)

NIS (originalmente conocido como Yellow Pages) proporciona una base de datos de usuarios y grupos centralizada, permitiendo que un usuario inicie sesión con la misma identidad y contraseña en cualquier nodo del clúster.

* **Servidor NIS (en el nodo `nas`):**
    * Se instala el paquete `nis`.
    * Se define un nombre de dominio para el clúster (ej. `cluster`).
    * Se inicializa la base de datos de usuarios y grupos con `ypinit -m`.
    * Cada vez que se añade o modifica un usuario (`useradd`, `passwd`), es necesario regenerar la base de datos con el comando `make -C /var/yp`.

* **Clientes NIS (en `Master` y `Servers`):**
    * Se instala el paquete `nis`.
    * Se configura el archivo `/etc/yp.conf` para apuntar al servidor NIS (`nas`).
    * Se edita el archivo `/etc/nsswitch.conf` para indicarle al sistema que, además de los archivos locales, debe consultar `nis` para validar usuarios (`passwd`), grupos (`group`) y contraseñas (`shadow`).
