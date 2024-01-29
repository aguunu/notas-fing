La estructura de la red se divide en capas, donde cada una de estas implementa un servicio. Esta división permite trabajar con sistemas más complejos.

## Modelo TCP/IP
1. [[Capa de Aplicación]]: Soporte de aplicaciones en red *(ej. FTP, SMTP, HTTP, DNS, P2P)*.
2. [[Capa de Transporte]]: Transferencia de los datos *(ej. TCP, UDP)*.
3. [[Capa de Red]]: Rutear los *datagramas* de la fuente hasta el destino *(ej. IP, protocolos de enrutamiento)*.
4. [[Capa de Enlace]]: Transferir los datos entre elementos de red vecinos *(ej. ethernet, 802.111, PPP).*
5. [[Capa Física]]: Trasferir los bits mediante un [[#Enlace Físico]] *(ej. Fibra Óptica)*.

## Modelo ISO/OSI
Es una modificación del [[#Modelo TCP/IP]], agregando las siguientes capas luego de la [[Capa de Aplicación]].
- Presentación: Permite a las aplicaciones interpretar el significado de los datos, por ejemplo, encriptación, compresión, etc.
- Sesión: Sincronización, checkpointing, recuperación de datos, etc.