El [[Protocolo]] TCP (Transmission Control Protocol), permite crear conexiones entre entre distintos servicios. Proporciona un mecanismo para distinguir distintos servicios dentro de una misma máquina, a través del concepto de *port*. El protocolo posee las siguientes características:
- Orientado a Conexión: TCP intercambia entre el cliente y el servidor información de control de la capa de transporte antes de que los mensajes a nivel de aplicación empiecen a fluir. Una vez están preparados, se dice que existe una conexión TCP entre los sockets de ambos procesos.
- Transporte Confiable: TCP garantiza que el total de los datos van a ser transferidos sin error y en orden correcto.
- Control de Flujo: El emisor no va a "abrumar" al receptor con la cantidad de datos transferidos.
- Control de Congestión: Apura al emisor cuando la red está sobrecargada.

*Nota: el protocolo TCP no provee control de tiempo, garantías de [[Network#Throughput|Throughput]]* mínimo, seguridad.

>[!info] 
>El protocolo TCP da soporte a gran parte de las aplicaciones de Internet (navegadores, intercambio de archivos, clientes FTP, etc.) y protocolos de aplicación (HTTP, SMTP, SSH, FTP).
