El [[Protocolo]] TCP (Transmission Control Protocol) permite la transmisión de datos mediante una conexión *full-duplex* entre un único emisor y un único receptor, permitiendo crear conexiones entre distintos servicios dentro de un mismo *host* mediante el concepto de *port*. 

>[!info] Maximum Segment Size
>La conexión posee un tamaño máximo de segmento (MSS), el cual es definido dependiendo del tamaño del [[Ethernet#Ethernet Frame|Frame]] más grande que puede ser enviado por el host emisor local, y luego considerando que el tamaño paquete TCP y además el largo del encabezado TCP/IP entren en un único frame de capa de enlace.

El protocolo posee las siguientes características:
- Orientado a Conexión: TCP intercambia entre el cliente y el servidor información de control de la capa de transporte antes de que los mensajes a nivel de aplicación empiecen a fluir. Una vez están preparados, se dice que existe una conexión TCP entre los sockets de ambos procesos.
- Transporte Confiable: TCP garantiza que el total de los datos van a ser transferidos sin error y en orden correcto.
- Control de Flujo: El emisor no va a "abrumar" al receptor con la cantidad de datos transferidos.
- Control de Congestión: Apura al emisor cuando la red está sobrecargada.


>[!info] 
>El protocolo TCP da soporte a gran parte de las aplicaciones de Internet (navegadores, intercambio de archivos, clientes FTP, etc.) y protocolos de aplicación (HTTP, SMTP, SSH, FTP).

```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |          Source Port          |       Destination Port        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                        Sequence Number                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Acknowledgment Number                      |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Data |       |C|E|U|A|P|R|S|F|                               |
   | Offset| Rsrvd |W|C|R|C|S|S|Y|I|            Window             |
   |       |       |R|E|G|K|H|T|N|N|                               |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |           Checksum            |         Urgent Pointer        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                           [Options]                           |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                                                               :
   :                             Data                              :
   :                                                               |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- *Sequence Number*: Es el número de secuencia que identifica al primer byte del segmento dentro del *byte-stream*.
- *Acknowledgement Number (ACK)*: Es el número de secuencia que identifica al byte esperado dentro del *byte-stream* desde el otro lado de la conexión. *Notar: el ACK es acumulativo.*

## Round Trip Time
El *round trip time (RTT)* es el tiempo transcurrido entre que un segmento es enviado y luego se recibe su ACK.

TCP utiliza un mecanismo de *timeout* para la recuperación de segmentos perdidos. El valor del *timeout* depende de la implementación de TCP. Para calcular el valor óptimo del *timeout* se debe estimar el RTT. Para esto se utiliza una muestra ignorando retransmisiones $SampleRTT$ (que puede variar entre los segmentos dependiendo las circunstancias) y luego se obtiene una estimación más precisa con la siguiente formula:
$$EstimatedRTT = (1 - \alpha) \cdot EstimatedRTT + \alpha \cdot SampleRTT$$
Donde el valor de $\alpha$ recomendado es $\alpha=0.125$.

Luego se calcula la desviación de $SampleRTT$ con $EstimatedRTT$,
$$DevRTT = (1 - \beta) \cdot DevRTT + \beta \cdot |SampleRTT - EstimatedRTT|$$
Donde el valor de $\beta$ recomendado es $\beta = 0.25$.

Por último se calcula el valor del $Timeout$ es:
$$Timeout = EstimatedRTT + 4 \cdot DevRTT$$

## Reliable Data Transfer
TCP implementa los autómatas *rdt* sobre un servicio IP no confiable, asegurándose que cada byte que envía el emisor es idéntico al byte que recibe el receptor.

### Generación de ACKs
#TODO

### Retransmisión Rápida
Consiste en detectar paquetes perdidos antes de que ocurra el timeout utilizando *duplicated ACKs*, es decir, *ACKs* correspondientes a segmentos que ya habían recibido su *ACK*. Por ende, si el emisor recibe 3 *duplicated ACKs* este supone que el segmento se perdió y realiza una retransmisión sin haber culminado el *timeout* del mismo.

### Control de Flujo
El receptor almacena los datos recibidos en un *buffer* que posteriormente será consumido por la [[Capa de Aplicación]]. Esto puede ocasionar que el *buffer* se desborde, generando pérdidas de información. Para evitar este problema, TCP empareja la tasa de envío de datos del emisor con la tasa de lectura de datos sobre el *buffer*.

Sea $\texttt{RecvBuffer}$ el tamaño del buffer $\texttt{LastByteRecv}$ el número del último byte del *byte stream* recibido y $\texttt{LastByteRead}$ el número del último byte del *byte stream* leído. Tenemos la siguiente ecuación:
$$\texttt{LastByteRecv} - \texttt{LastByteRead} \leq \texttt{RecvBuffer}$$
Luego, la ventana de recepción $(\texttt{rwnd})$ es definida como la cantidad de espacio disponible en el *buffer*.
$$\texttt{rwnd} = \texttt{RecvBuffer} - |\texttt{LastByteRecv} - \texttt{LastByteRead}|$$
Donde el receptor indica el espacio disponible en su *buffer* enviando en el segmento el valor $\texttt{rwnd}$.

<iframe style="border-radius: 15px; background: #FFFFFFAA; height: 70vh; width: 100%;" src=https://computerscience.unicam.it/marcantoni/reti/applet/FlowControl/flow.html></iframe>

### Manejo de Conexiones
TCP es un protocolo orientado a conexión, por lo cual, el emisor y receptor establecen dicha conexión antes de comenzar a intercambiar segmentos. Eso se logra mediante *three-way handshake*.

#### Inicio de Conexión
Se denomina *three-way handhake* al inicio de una conexión TCP.
1. $A \rightarrow B:$ $A$ envía un segmento a $B$ con la *flag* $\texttt{SYN}$ activa. Además, se índica el número de secuencia inicial $(\texttt{client\_isn})$.
2. $B \rightarrow A :$ cuando el segmento es recibido por $B$, este asigna memoria a los buffers, inicializa las variables, especifica el número de secuencia inicial del servidor $(\texttt{server\_isn})$ y luego responde con un segmento con las *flags* $\texttt{SYN}$ y $\texttt{ACK}$ activas, siendo el campo $\texttt{acknowledgment}$ igual a $\texttt{client\_isn + 1}$, y el campo $\texttt{sequence}$ igual a $\texttt{server\_isn}$.
3. $A \rightarrow B :$ cuando el segmento es recibido por $A$, este responde con un segmento con la *flag* $\texttt{ACK}$  activa, siendo el campo $\texttt{acknowledgment}$ igual a $\texttt{server\_isn + 1}$, además de poder incluir datos de la [[Capa de Aplicación]].

>[!attention] 
>En los pasos $(1)$ y $(2)$ los segmentos que se utilizan NO pueden contener datos de la [[Capa de Aplicación]].

#### Cierre de Conexión
Se denomina *four-way handshake* al cierre de una conexión TCP.
1. $A \rightarrow B :$ *I have $\texttt{\textcolor{green}{FIN}ished}$ sending data, my las sequence number is $\texttt{X}$*.
2. $A \leftarrow B :$ *I $\texttt{\textcolor{red}{ACK}nowledge}$ receiving your $\texttt{FIN}$ with $\texttt{ACK\# = [X+1]}$.*
3. $A \leftarrow B :$ *I have $\texttt{\textcolor{green}{FIN}ished}$ sending data, my last sequence number is $\texttt{Y}$.*
4. $A \rightarrow B :$ *I $\texttt{\textcolor{red}{ACK}nowledge}$ receiving your $\texttt{FIN}$ with $\texttt{ACK\# = [Y+1]}$.*
*Notar: Si el host $B$ lo desea, puede seguir transmitiendo datos entre los pasos $(2)$ y $(3)$.*

>[!warning] Phantom Byte
>En el envío de segmentos con la *flag* $\texttt{SYN}$ o $\texttt{FIN}$ activa, a pesar de que se envían 0 bytes de datos, el número de secuencia deberá incrementar, pues en otro caso, el emisor del segmento podría confundir el $\texttt{ACK}$ que quedará esperando por el $\texttt{ACK}$ anterior.

