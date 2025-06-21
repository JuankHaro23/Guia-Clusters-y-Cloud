## Despliegue de Infraestructura en AWS EC2

[cite_start]La base para trabajar en AWS es el servicio **Elastic Compute Cloud (EC2)**, que permite el aprovisionamiento de máquinas virtuales (instancias).

### Conceptos Clave:
* **AMI (Amazon Machine Image):** Plantillas pre-configuradas con un SO y software. [cite_start]Usamos AMIs de Bitnami con LAMP para un despliegue rápido.
* **Pares de Claves (Key Pairs):** Par de claves pública/privada para la autenticación segura vía SSH sin contraseñas. [cite_start]La clave privada se gestiona localmente y la pública se inyecta en la instancia.
* **Grupos de Seguridad (Security Groups):** Actúan como un firewall virtual que controla el tráfico de entrada y salida de las instancias. [cite_start]Configuramos reglas para permitir tráfico en los puertos 22 (SSH) y 80 (HTTP).
