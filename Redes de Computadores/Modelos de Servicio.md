La estructura de la red se divide en capas, donde cada una de estas implementa un servicio. Esta división permite trabajar con sistemas más complejos.

## Modelo TCP/IP
1. Aplicación: Soporte de aplicaciones en red *(ej. FTP, SMTP, HTTP, DNS, P2P)*.
2. Transporte: Transferencia de los datos *(ej. TCP, UDP)*.
3. Red: Rutea los *datagramas* de la fuente hasta el destino *(ej. IP, protocolos de enrutamiento)*.
4. Enlace: Transferir los datos entre elementos de red vecinos *(ej. ethernet, 802.111, PPP).*
5. Física: Trasferir los bits mediante un [[#Enlace Físico]] *(ej. Fibra Óptica)*.

## Modelo ISO/OSI
Es una modificación del [[#Modelo TCP/IP]], agregando las siguientes capas luego de la capa de *Aplicación*.
- Presentación: Permite a las aplicaciones interpretar el significado de los datos, por ejemplo, encriptación, compresión, etc.
- Sesión: Sincronización, checkpointing, recuperación de datos, etc.