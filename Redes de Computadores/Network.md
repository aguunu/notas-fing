Es un conjunto de computadoras conectadas entre si cuyo fin es compartir recursos haciendo uso de [[Protocolo|Protocolos]] que permiten la comunicación sobre la red.

## Network Edges
Se refiere a los dispositivos que se encuentran en el borde de la red **(End Systems)**, es decir, aquellos dispositivos que ejecutan aplicaciones como el navegador web, E-Mail, etc.

### Access Network
Hace referencia a la red que se encarga de conectar físicamente un *end system* con un primer *router* **(Edge Router)**.

>[!question] ¿Cómo se conectan los *end systems* a un *edge router*?
>- Residential Access Networks
>- Institutional Access Networks
>- Mobile Access Networks

### Tecnologías de Acceso
- Home Access
	- DSL (Digital Subscriber Line)
	- Cable
	- FTTH (Fiber to the Home)
	- Dial-Up
	- Satellite
- Enterprise Access (And Home)
	- Ethernet
	- WIFI
- Wide-Area Wireless Access
	- 3G/4G/5G
	- LTE

### Enlace Físico
Los enlaces físicos pueden clasificarse en dos categorías:
- Guided Media
	- Twisted Pair (TP)
	- Coaxial Cable
	- Fiber Optic Cable
- Unguided Media: No posee un "cable físico". Por lo general, la señal tiende a ser *broadcast*, es decir, no se emite a un receptor en especifico.
	- Wireless Radio: La señales se comunican a través de bandas que se encuentran en el *espectro electromagnético*.
		- Wireless LAN (Local Access Network) (WIFI)
		- Wide-Area *(e.g. 4G)*
		- Bluetooth
		- Terrestrial Microwave
		- Satellite

Por otra parte, también se clasifican según el *duplex* de la comunicación:
![[Drawing 2023-09-20 11.08.41.excalidraw|center]]

## Network Core
Es una red de *routers* interconectados para la transmisión de datos entre los distintos *end systems*. Esta transmisión se realiza mediante [[#Packet-Switching]] o [[#Circuit-Switching]].

### Packet-Switching
Los datos se dividen en [[Data Packets]]. Los paquetes del usuario $A$ y $B$ comparten los mismos recursos de la red. Además, cada paquete ocupa un *bandwidth* completo del enlace, y los recursos son utilizados a medida que son requeridos.

>[!warning] Contención de Recursos
>- *Almacenamiento & Reenvío*: los nodos deben recibir el paquete en su totalidad antes de transmitirlo al siguiente enlace.
>- *Congestión*: se genera una cola de paquetes para el uso del enlace.

### Circuit-Switching
Se establece un canal de comunicaciones dedicado entre dos estaciones. Luego, utilizando técnicas de división de señales sobre el mismo medio, varios "llamados" podrán ser atendidos en simultaneo. *Notar: Un canal puede quedar ocioso, es decir, no existe una "llamada" que lo este usando, esto implica desperdiciar recursos de la red.*
- **Frequency Division Multiplexing (FDM)**: Divide el *bandwidth* en un conjunto de frecuencias que no se sobrepone entre ellas **(Frequency Bands)**, de esta forma, permitiendo trasmitir varios flujos de datos sobre el mismo enlace físico.
- **Time Division Multiplexing (TDM)**: Multiples frecuencias se colocan sobre el mismo enlace físico separando cada una de estas en segmentos que poseen una corta duración sobre el enlace físico.

## Throughput
Indica la velocidad en que los datos se transmiten sobre un canal de comunicación entre un emisor y receptor en un instante de tiempo determinado. *Nota: Su unidad de medida es (bits/unidad de tiempo).*

## Bandwidth
Indica la cantidad máxima de datos que pueden ser trasmitidos sobre un canal de comunicación en un instante de tiempo determinado. *Nota: Su unidad de medida es (bits/unidad de tiempo).*

## Network of Networks
#TODO 