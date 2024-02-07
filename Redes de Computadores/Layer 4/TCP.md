El [[Protocolo]] TCP (Transmission Control Protocol) permite la transmisión de datos mediante una conexión *full-duplex* entre un único emisor y un único receptor, permitiendo crear conexiones entre distintos servicios dentro de un mismo *host* mediante el concepto de *port*.

La conexión posee un $\texttt{MSS}$ *(maximum segment size)*, el cual se define al iniciar una conexión TCP y representa el tamaño máximo de un *TCP segment* que puede ser emitido por la red. Este valor puede ser calculado con la siguiente formula:
$$\texttt{MSS} = \texttt{MTU} - (\texttt{IP\_HEADER} + \texttt{TCP\_HEADER})$$

El protocolo posee las siguientes características:
- Orientado a Conexión: TCP intercambia entre el cliente y el servidor información de control de la capa de transporte antes de que los mensajes a nivel de aplicación empiecen a fluir. Una vez están preparados, se dice que existe una conexión TCP entre los sockets de ambos procesos.
- Transporte Confiable: TCP garantiza que el total de los datos van a ser transferidos sin error y en orden correcto.
- Control de Flujo: El emisor no va a "abrumar" al receptor con la cantidad de datos transferidos.
- Control de Congestión: Apura al emisor cuando la red está sobrecargada.

![[Drawing 2024-01-30 15.44.55.excalidraw]]
- *Sequence Number*: Es el número de secuencia que identifica al primer byte del segmento dentro del *byte-stream*.
- *Acknowledgement Number (ACK)*: Es el número de secuencia que identifica al byte esperado dentro del *byte-stream* desde el otro lado de la conexión. *Notar: el ACK es acumulativo.*

## Reliable Data Transfer
TCP implementa los autómatas *rdt* sobre un servicio IP no confiable, asegurándose que cada byte que envía el emisor es idéntico al byte que recibe el receptor.

## Round Trip Time
El *round trip time (RTT)* es el tiempo transcurrido entre que un segmento es enviado y se recibe el ACK correspondiente.

TCP utiliza un mecanismo de *timeout* para la recuperación de segmentos perdidos. Para calcular el valor óptimo del *timeout* se debe estimar el RTT. Para esto se utiliza una muestra ignorando retransmisiones $SampleRTT$ (que puede variar entre los segmentos dependiendo las circunstancias) y luego se obtiene una estimación más precisa con la siguiente formula:
$$EstimatedRTT = (1 - \alpha) \cdot EstimatedRTT + \alpha \cdot SampleRTT$$
Donde el valor de $\alpha$ recomendado es $\alpha=0.125$.

Luego se calcula la desviación de $SampleRTT$ con $EstimatedRTT$,
$$DevRTT = (1 - \beta) \cdot DevRTT + \beta \cdot |SampleRTT - EstimatedRTT|$$
Donde el valor de $\beta$ recomendado es $\beta = 0.25$.

Por último se calcula el valor del $Timeout$ es:
$$Timeout = EstimatedRTT + 4 \cdot DevRTT$$

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

## Control de Congestión
Para evitar la congestión en la red, TCP utiliza una algoritmo de control de congestión que incluye principios de *AIMD*, *slow start* y *congestion window*.

**AIMD *(additive increase multiplicative decrease)***
- *additive increase*: el emisor aumenta su $\texttt{cwnd}$  *(congestion window)* en $\texttt{1 MSS}$ *(maximum segment size)* por cada $\texttt{RTT}$ *(round trip time)* hasta que ocurre una perdida (esto último se logra al recibir un $\texttt{ACK}$).
-  *multiplicative decrease*: al ocurrir una perdida, su $\texttt{cwnd}$ se divide a la mitad.

**Congestion Window**
La *congestion window* es mantenida por el emisor, y se trata de un método para evitar que se sature el link que se encuentra entre el emisor y el receptor.

$$\texttt{LastByteSent} - \texttt{LastByteACKed} \leq \texttt{cwnd}$$

>[!warning] 
>This should not be confused with the *sliding window* maintained by the sender which exists to prevent _the receiver_ from becoming overloaded.

Inicialmente empieza en la etapa de *slow start* con un valor de $\texttt{cwnd}$ igual a un $\texttt{MSS}$. Luego, por cada $\texttt{ACK}$ recibido $\texttt{cwnd}$ es incrementado por 1 $\texttt{MSS}$.

La tasa de transmisión seguirá aumentando exponencialmente mientras no ocurra alguno de los siguientes eventos:
- Se detecte *packet loss*.
- $\texttt{rcvw}$ *(receiver window)* se convierta en el limitante.
- Se alcance el $\texttt{ssthresh}$ *(slow start threshold)*.

Cuando el valor de $\texttt{cwnd}$ alcanza el $\texttt{ssthresh}$, empieza la etapa de *congestion avoidance*. Incrementando el valor de $\texttt{cwnd}$ de forma casi lineal: $$\texttt{cwnd} = \texttt{cwnd} + \texttt{MSS} \cdot (\texttt{MSS}/\texttt{cwnd})$$
Al detectarse un *packet loss*:
- *TCP Tahoe*
	- $\texttt{ssthreshold} = \frac{\texttt{cwnd}}{2}$
	- Si se trata de *timeout*, $\texttt{cwnd}=1$.
	- Si se trata de tres *duplicated ACK*, $\texttt{cwnd}=1$.
	- Se vuelve a la etapa de *slow start*.
- *TCP Reno*
	- $\texttt{ssthreshhold} = \frac{\texttt{cwnd}}{2}$
	- Si se trata de *timeout*, $\texttt{cwnd}=1$, volviendo a la etapa de *slow start*.
	- Si se trata de tres *duplicated ACK*, $\texttt{cwnd} = \frac{\texttt{cwnd}}{2}$, pasa a la etapa *fast-recovery* donde realiza *fast retransmission*, es decir, reenvía el paquete sin haber culminado su timeout correspondiente. En este estado, por cada *duplicated ACK*, aumenta $\texttt{cwnd}$ en un $\texttt{MSS}$. Luego, al llegar un $\texttt{ACK}$ se vuelve a la etapa de *congestion avoidance* salteando la etapa de *slow start*.

>[!note] 
>TCP envía $\texttt{cwnd}$ bytes, espera $\texttt{RTT}$ para recibir el $\texttt{ACK}$ y envía más bytes. Por ende, la tasa de transmisión se puede calcular como: $$rate \approx \frac{\texttt{cwnd}}{\texttt{RTT}} \text{bytes/sec}$$

### Three-Way Handshake
Se denomina *three-way handshake* al inicio de una conexión TCP.
1. $A \rightarrow B:$ $A$ envía un segmento a $B$ con la *flag* $\texttt{SYN}$ activa. Además, se índica el número de secuencia inicial $(\texttt{client\_isn})$.
2. $B \rightarrow A :$ cuando el segmento es recibido por $B$, este asigna memoria a los buffers, inicializa las variables, especifica el número de secuencia inicial del servidor $(\texttt{server\_isn})$ y luego responde con un segmento con las *flags* $\texttt{SYN}$ y $\texttt{ACK}$ activas, siendo el campo $\texttt{acknowledgment}$ igual a $\texttt{client\_isn + 1}$, y el campo $\texttt{sequence}$ igual a $\texttt{server\_isn}$.
3. $A \rightarrow B :$ cuando el segmento es recibido por $A$, este responde con un segmento con la *flag* $\texttt{ACK}$  activa, siendo el campo $\texttt{acknowledgment}$ igual a $\texttt{server\_isn + 1}$, además de poder incluir datos de la [[Capa de Aplicación]].

>[!attention] 
>En los pasos $(1)$ y $(2)$ los segmentos que se utilizan NO pueden contener datos de la [[Capa de Aplicación]].

### Four-Way Handshake
Se denomina *four-way handshake* al cierre de una conexión TCP.
1. $A \rightarrow B :$ *I have $\texttt{\textcolor{green}{FIN}ished}$ sending data, my las sequence number is $\texttt{X}$*.
2. $A \leftarrow B :$ *I $\texttt{\textcolor{red}{ACK}nowledge}$ receiving your $\texttt{FIN}$ with $\texttt{ACK\# = [X+1]}$.*
3. $A \leftarrow B :$ *I have $\texttt{\textcolor{green}{FIN}ished}$ sending data, my last sequence number is $\texttt{Y}$.*
4. $A \rightarrow B :$ *I $\texttt{\textcolor{red}{ACK}nowledge}$ receiving your $\texttt{FIN}$ with $\texttt{ACK\# = [Y+1]}$.*
*Notar: Si el host $B$ lo desea, puede seguir transmitiendo datos entre los pasos $(2)$ y $(3)$.*

>[!warning] Phantom Byte
>En el envío de segmentos con la *flag* $\texttt{SYN}$ o $\texttt{FIN}$ activa, a pesar de que se envían 0 bytes de datos, el número de secuencia deberá incrementar, pues en otro caso, el emisor del segmento podría confundir el $\texttt{ACK}$ que quedará esperando por el $\texttt{ACK}$ anterior.

