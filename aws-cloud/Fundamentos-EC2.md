## Fundamentos de EC2: Instancias, Redes y Seguridad

[cite_start]**Amazon EC2 (Elastic Compute Cloud)** es el servicio central de AWS para la computación en la nube, permitiendo el despliegue de máquinas virtuales (instancias) bajo un modelo de Infraestructura como Servicio (IaaS).

### Componentes Esenciales

* [cite_start]**AMI (Amazon Machine Image):** Son plantillas pre-configuradas que contienen un sistema operativo y software para crear una instancia. [cite_start]Existen imágenes basadas en EBS (con almacenamiento persistente) y en S3 (efímeras). [cite_start]Para los laboratorios, se utilizan AMIs de Bitnami que incluyen pilas de software como LAMP.

* [cite_start]**Par de Claves (Key Pair):** Es un conjunto de credenciales de seguridad (clave pública y privada) usado para la autenticación en las instancias vía SSH sin necesidad de contraseña. [cite_start]La clave pública se almacena en AWS y se inyecta en la instancia al lanzarla, mientras que el usuario guarda de forma segura la clave privada.

* [cite_start]**Grupos de Seguridad (Security Groups):** Actúan como un firewall virtual para controlar el tráfico de red de entrada y salida. [cite_start]Se definen reglas para permitir el acceso a puertos específicos, como el puerto 22 (SSH) y el 80 (HTTP), desde orígenes definidos (ej. una IP específica o cualquier lugar de Internet).

### Flujo de Despliegue

1.  **Creación de Recursos Previos:** Se crea un **Par de Claves** para el acceso y un **Grupo de Seguridad** con las reglas de firewall necesarias.
2.  **Lanzamiento de la Instancia:**
    * Se selecciona una **AMI** (ej. "Bitnami LAMP").
    * [cite_start]Se elige un **Tipo de Instancia** (ej. `t3.micro`), que define los recursos de CPU y RAM.
    * Se configura la **Red**, seleccionando un VPC y una subred pública para que la instancia sea accesible desde Internet.
    * [cite_start]Se asocian el **Par de Claves** y el **Grupo de Seguridad** creados previamente.
3.  **Conexión y Uso:**
    * [cite_start]Una vez la instancia está en estado *running*, se puede acceder a ella usando su IP pública o nombre DNS.
    * [cite_start]La conexión se realiza mediante un cliente SSH, utilizando la clave privada y el nombre de usuario adecuado para la AMI (ej. `bitnami`).

[cite_start]Las instancias basadas en EBS pueden ser detenidas (pausando el coste de cómputo) y reiniciadas, conservando los datos de su disco raíz, aunque reciben una nueva IP pública al volver a arrancar.
