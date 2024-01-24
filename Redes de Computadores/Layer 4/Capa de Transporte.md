La funcionalidad de la capa de transporte es proveer comunicación lógica entre [[Procesos]] que se encuentran en ejecución sobre distintos *hosts*.

Podemos clasificar a los *end systems* según su rol:
- *Emisor:* divide mensajes de la aplicación en *segmentos*, luego, los envía a la [[Capa de Red]].
- *Receptor:* se encarga de convertir los *segmentos* en mensajes, luego, los envía a la [[Capa de Aplicación]].

>[!note] 
>Al crear *sockets*, se deberá especificar cierto *port number* del *host*.

Las acciones que realiza un *emisor* son las siguientes:
1. Recibe un mensaje desde la [[Capa de Aplicación]].
2. Determina los *headers* de los segmentos.
3. Crea los segmentos.
4. Envía los segmentos a la [[Capa de Red]].

Mientras que las acciones que realiza un *receptor* son las siguientes:
1. Recibe un segmento desde la [[Capa de Red]].
2. Chequea los valores del *header*.
3. Extra el mensaje de la [[Capa de Aplicación]].
4. Realiza *demultiplexing* para enviar el mensaje en orden correcto a la [[Capa de Aplicación]] mediante cierto *socket* identificado por su *port number*.

![[Drawing 2023-08-15 15.16.30.excalidraw|center]]

Existen dos protocolos disponibles en esta capa, [[TCP]] y [[UDP]].

## Multiplexing & Demultiplexing
El *multiplexing* y *demultiplexing* consiste en extender el servicio de comunicación host-to-host de la capa de red, a un servicio de comunicación process-to-process para los servicios ejecutandose en los hosts.

>[!question] ¿Cómo funciona *demultiplexing*?
>El host recibe *IP datagrams*, cada *datagram* posee el *source IP address* y *destination IP address*. Por otro lado, cada *datagram* posee 1 *tranport-layer segment*, donde cada uno de estos posee *source port* y *destination port*.
>
>De esta forma, el *host* utiliza *IP addresses* & *port numbers* para dirigir el *segmento* al *socket* apropiado.

Podemos identificar dos tipos de *demultiplexing* según el protocolo perteneciente a la *capa de transporte* que se este utilizando.
- Sin Conexión ([[UDP]]): El socket se identifica con el puerto destino. Cuando se crea un datagrama, se especifica tanto el puerto origen como destino. Cuando un host recibe un segmento UDP, este chequea el puerto destino en el segmento y luego dirige este segmento al socket asociado con dicho puerto. *Nota: los datagramas con mismo puerto de destino, pero diferente IP y/o puerto origen serán dirigidos al mismo socket del host receptor.*
- Orientado a Conexión ([[TCP]]): El socket se identifica con una 4-upla *(IP origen, puerto origen, IP destino, puerto destino).* *Nota: los hosts servidores deben ser capaces de soportar varios sockets TCP simultáneos, cada uno de estos, representado por su 4-upla.*

![[Drawing 2023-08-15 15.07.55.excalidraw|center]]