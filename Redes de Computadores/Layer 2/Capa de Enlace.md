La *network interface card (NIC)* es el dispositivo encargado de implementar la capa de enlace. A este dispositivo se lo conoce como nodo. Además, los canales de comunicación que conectan nodos adyacentes se los conoce como enlaces.

A través de un [[Enlace]], un nodo transmisor encapsula el datagrama en un *link-layer frame* y lo transmite mediante el enlace.

## Detección y Corrección de Errores
- *[[Detección y Corrección de Errores#Paridad de 1 bit|Single Bit Parity]]: detecta un único bit erróneo.*
- *Two Dimensional Bit Parity: detecta y corrige un único bit erróneo.*
- *[[Detección y Corrección de Errores#Checksum|Checksum]]: detecta errores. Notar: se utiliza únicamente en [[Capa de Transporte]].*
- *[[Detección y Corrección de Errores#Cyclic Redundancy Check|Cyclic Redundancy Check (CRC)]]: detecta errores.*

## Dominio de Colisión
Un *dominio de colisión* es un conjunto de nodos que pueden sufrir colisiones entre ellos al enviar un [[Ethernet#Ethernet Frame|Frame]]. Un [[Enlace]] en donde pueden ocurrir colisiones define un *dominio de colisión*. Por lo tanto, un [[Enlace#Enlace Broadcast|Enlace Broadcast]] define un *dominio de colisión*.

## Dominio de Broadcast
Un *dominio de broadcast* es un conjunto de nodos que forman parte de una LAN. Además, a todos estos nodos son capaces de recibir el mismo [[Ethernet#Ethernet Frame|Frame]] cuya [[MAC Address|MAC]] destino es `FF-FF-FF-FF-FF-FF`.
