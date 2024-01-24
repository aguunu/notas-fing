Un *enlace de broadcast* puede tener múltiples nodos emisor y receptor, todos conectados al mismo canal de broadcast único y compartido. *(ej. Ethernet, HFC y 802.11)*.

Los *Multiple Access Protocols* determinan cómo varios nodos comparten y acceden a un medio de transmisión compartido, como un canal de comunicación o una red, en este caso a un enlace de broadcast. Produciéndose una colisión cuando un nodo recibe dos o más señales al mismo tiempo.

Por ende, un *Multiple Access Protocol* ideal para un enlace de broadcast con tasa de $R \; bps$ debe cumplir con las siguientes características:
- Cuando $M$ nodos tiene datos para enviar, cada uno de ellos tiene un throughput de $\frac{R}{M} \; bps$.
- Totalmente descentralizado, es decir, no hay un nodo maestro que representa un punto de fallo único para la red (no hay un nodo especial para coordinar la transmisión, ni tampoco hay sincronización de reloj o slots).
- El protocolo debe ser simple, de forma que no sea costoso de implementar.

## Channel Partitioning
- Time Division Multiple Access: Se accede al canal en “rondas”. Cada estación tiene un slot de largo fijo (tiempo de transmisión del paquete) en cada ronda. Los slots sin usar quedan ociosos.
- Frecuency Division Multiple Access: El espectro del canal se divide en bandas de frecuencia. Cada estación tiene asignada una banda de frecuencia fija. Los tiempos de transmisión en bandas de frecuencia sin utilizar quedan ociosos.

## Random Access
### Slotted ALOHA
El protocolo *slotted ALOHA* hace las siguientes suposiciones:
- Todos los frames tienen el mismo tamaño.
- El tiempo se divide en slots de igual tamaño (el tiempo para transmitir un frame).
- Los nodos empiezan a transmitir solo el comienzo del slot.
- Nodos sincronizados.
- Si 2 o más nodos transmite en un slot, todos los nodos detectan la colisión.

Al transmitir un nuevo frame en el siguiente slot:
- Si no hay colisión, el nodo puede enviar un nuevo frame en el siguiente slot.
- Si hay colisión, el nodo retransmite el frame en cada slot subsecuente con probabilidad $p$ hasta que haya éxito.

### Pure (Unslotted) ALOHA
A diferencia de [[#Slotted ALOHA]] cuando un nodo tiene un frame para transmitir, lo transmite en cualquier momento sin esperar.

### CSMA
CSMA (Carrier Sense Multiple Access) cumple con las siguientes reglas:
- *Carrier Sensing:* Antes de iniciar una transmisión, un nodo que desea transmitir primero "escucha" el medio para determinar si está ocupado o libre.
- *Collision Detection:* Si un nodo que se encuentra transmitiendo detecta interferencia, para de transmitir y espera una cantidad de tiempo aleatoria antes de repetir el ciclo.

>[!error] 
>Estas reglas no implica que no puedan ocurrir colisiones, ya que el retraso de propagación implica que dos nodos puedan no escuchar la transmisión del otro.

### CSMA/CD
CSMA/CD (Carrier Sense Multiple Access / Collision Detection) es una mejora de [[#CSMA]] que incorpora la detección y manejo de colisiones durante la transmisión.

Si durante la transmisión el nodo detecta una colisión, envía una *jam signal*. Luego, el nodo entra en *binary (exponential) backoff* esperando un tiempo aleatorio antes de intentar transmitir nuevamente (este tiempo aumenta exponencialmente), reduciendo la probabilidad de otra colisión.

1. NIC recibe un datagrama de la capa de red y crea un frame.
2. Si la NIC siente un canal ocioso, comienza la transmisión. Si la NIC siente un canal ocupado, espera hasta que el canal quede ocioso y luego transmite.
3. Si la NIC transmite el frame entero sin detectar otra transmisión, entonces la NIC completo su trabajo para ese frame.
4. Si la NIC detecta otra transmisión mientras está transmitiendo, aborta y envía una señal de atasco.
5. Luego de abortar, la NIC entra a *Exponential Backoff*.
	- *Exponential Backoff*: luego de la *n-ésima* colisión, la NIC elige un $K \in \{0,1, .., 2^n - 1\}$ de forma aleatoria y procede a esperar $K \cdot 512 \textit{ bit times }$ y regresa al paso 2.

## Taking Turns
- Polling Protocol: Un nodo master invita a los nodos esclavos a transmitir en turnos.
- Token Passing Protocol: Un token de control se pasa de un nodo a otro en forma secuencial.