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

## Goodput
Es la velocidad a la que los __datos útiles__ atraviesan un [[Enlace]]. *Notar: el goodput contempla únicamente los datos útiles, es decir, los datos enviados desde [[Capa de Aplicación]].*

## Throughput
Es la velocidad a la que los datos atraviesan un [[Enlace]]. *Notar: el throughput contempla las retransmisiones, flow control, congestion avoidance, así como también los datos de los headers.*

## Bandwidth
Es la velocidad máxima a la que los datos pueden atravesar un [[Enlace]]. Por ende, podemos deducir la siguiente ecuación:

$$\texttt{Goodput} < \texttt{Throughput} \leq \texttt{Bandwidth}$$
