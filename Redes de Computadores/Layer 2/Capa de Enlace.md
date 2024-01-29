La *network interface card (NIC)* es el dispositivo encargado de implementar la capa de enlace. A este dispositivo se lo conoce como nodo. Además, los canales de comunicación que conectan nodos adyacentes se los conoce como enlaces.

A través de un [[Enlace]], un nodo transmisor encapsula el datagrama en un *link-layer frame* y lo transmite mediante el enlace.

## Detección y Corrección de Errores
- *[[Códigos y Errores#Paridad de 1 bit|Single Bit Parity]]: detecta un único bit erróneo.*
- *Two Dimensional Bit Parity: detecta y corrige un único bit erróneo.*
- *[[Códigos y Errores#Checksum|Checksum]]: detecta errores. Notar: se utiliza únicamente en [[Capa de Transporte]].*
- *CRC (Cyclic Redundancy Check):*

## Dominio de Colisión
Un [[Enlace]] en donde pueden ocurrir colisiones define un *dominio de colisión*. Por lo tanto,  un [[Enlace#Enlace Broadcast|Enlace Broadcast]] define un *dominio de colisión*.

## Dominio de Broadcast
El *dominio de broadcast* es la división lógica de la red dentro de la cual los nodos envían mensajes de broadcast. Dos nodos dentro del dominio de broadcast comparten *gateway*, dirección de subred y pueden transmitir a otro nodo dentro del dominio sin necesidad de enrutamiento; es decir, se encuentran en la misma LAN. Los dominios broadcast están delimitados por routers.


