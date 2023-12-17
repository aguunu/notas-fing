A cualquier dispositivo corriendo en capa de enlace lo denominaremos nodo. Además, a los canales de comunicación que conectan nodos adyacentes a lo largo del camino de comunicación como enlaces.

A través de un enlace, un nodo transmisor encapsula el datagrama en un *link-layer frame* y transmite el frame dentro del enlace. La *data-link layer frame* tiene la responsabilidad de transferir los datagramas desde un nodo al nodo físicamente adyacente a través de un enlace.

## Detección y Corrección de Errores

### Parity Check
- Single Bit Parity
- Two Dimensional Bit Parity
### Checksum
### Cyclic Redundancy Check (CRC)

## Enlace Punto a Punto
- *Enlace punto a punto*: consiste de un único emisor en uno de los extremos del enlace, y un único receptor, en el otro extremo del enlace. *(ej. PPP y HDLC)*.

## Dominio de Colisión
Se conoce como *dominio de colisión* al espacio físico con un ancho de banda compartido por un conjunto de nodos. En el caso que dos de esos nodos quieran transmitir al mismo tiempo, existe la posibilidad de que sus mensajes colisionen el espacio compartido y, o bien acaben convertidos en una amalgama de bits o bien no se pueda asegurar que al receptor le ha llegado el mensaje.

## Dominio de Broadcast
El *dominio de broadcast* es la división lógica de la red dentro de la cual los nodos envían mensajes de broadcast. Dos nodos dentro del dominio de broadcast comparten *gateway*, dirección de subred y pueden transmitir a otro nodo dentro del dominio sin necesidad de enrutamiento; es decir, se encuentran en la misma LAN. Los dominios broadcast están delimitados por routers.


