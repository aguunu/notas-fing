![[Drawing 2024-01-28 15.53.38.excalidraw|center]]

## Extension Header
Además del *header* principal, el protocolo define un conjunto de *extension header* que cumplen el rol del campo $\texttt{Options}$ definido en [[IPv4]]. Los *headers* se "enganchan" unos a otros sobre el campo $\texttt{Next Header}$.

![[Drawing 2024-01-30 15.56.12.excalidraw]]

### Fragment Header
Cualquier enlace que soporte IPv6 debe ser capaz de soportar un [[Maximum Transmission Unit|MTU]] de al menos 1280 bytes. En caso de que un nodo desee enviar paquetes mayores a 1280 bytes, este debe determinar el MTU mínimo admitido a lo largo de la ruta entre el origen y el destino utilizando *Path MTU*.

Si es necesario, el nodo origen es el encargado de fragmentar el paquete (agregando el *Fragment Header*) para poder ser enviado por la ruta.

![[Drawing 2024-01-30 16.05.31.excalidraw]]

>[!attention] 
>A diferencia de [[IPv4]], la fragmentación en [[IPv6]] es realizada UNICAMENTE por el nodo origen.

## IPv6 Address
Una *IPv6 address* es un dirección de 128 bits que pertenece a uno de los siguientes grupos:
- *unicast*
- *multicast*
- *anycast*

### Unicast Address
Una *unicast address* identifica una única interfaz.
- *`::/128` unspecified.*
- *`::1/128` loopback.
- *`2000::/3` global unicast:* identifica un interfaz en internet. Siguen el formato:
$$
\overset{3-bits}{{\overbrace{\texttt{001}}}} \cdot
\overset{45-bits}{{\overbrace{\texttt{Global-Routing-Prefix}}}} \cdot
\overset{16-bits}{{\overbrace{\texttt{Subnet-ID}}}} \cdot
\overset{64-bits}{{\overbrace{\texttt{Interface-ID}}}}
$$
- *`fc00::/7` unique local:* no son enrutables en internet. Por ende, son apropiadas por dispositivos que no tienen acceso a internet.
$$
\overset{7-bits}{{\overbrace{\texttt{Prefix}}}} \cdot
\overset{1-bits}{{\overbrace{\texttt{L}}}} \cdot
\overset{40-bits}{{\overbrace{\texttt{Global-ID}}}} \cdot
\overset{16-bits}{{\overbrace{\texttt{Subnet-ID}}}} \cdot
\overset{64-bits}{{\overbrace{\texttt{Interface-ID}}}}
$$
- *`fe80::/10` link local:* son utilizadas para la comunicación de nodos en un mismo link local. Por ende, no son enrutables más halla del link.
$$
\overset{10-bits}{{\overbrace{\texttt{1111111010}}}} \cdot
\overset{54-bits}{{\overbrace{\texttt{00...0}}}} \cdot
\overset{7-bits}{{\overbrace{\texttt{Interface-ID}}}} \cdot
$$
- *`::/80` embedded IPv4:* se incorpora una [[IPv4#IPv4 Address|IPv4]] dentro de una dirección IPv6, siguiendo el formato: $$
  \overset{96-bits}{{\overbrace{\texttt{00...0}}}} \cdot
  \overset{32-bits}{{\overbrace{\texttt{IPv4 address}}}}
$$
### Multicast Address
Una *multicast address* identifica a un grupo de interfaces. Un paquete cuyo destino es una dirección *multicast* es entregado a todos los nodos del *multicast group*. *Notar: utilizan el prefijo `ff00::/8`*
- *`ff00::/12` well-known*
- *`ff10:/12` transient*
- *`ff:02:0:0:0:0:1:ff00::/104` solicited-node*

>[!important] 
>El protocolo ==no define una dirección de tipo *broadcast*==. Sino que esta se implementa mediante *multicast*.

### Anycast Address
Una *anycast address* puede ser asignada a varias interfaces. Un paquete cuyo destino sea una *anycast address* es entregado a algún miembro del *anycast group.* *Notar: no posee prefijo especial.*

## Neighbor Discovery
Se definen los siguientes tipos de mensajes:
- *router solicitation (RS):*
- *router advertisement (RA):*
- *neighbor solicitation (NS):*
- *neighbor advertisement (NA):*
- *redirect:*

## Transición a IPv6
- Dual Stack
- Tunneling
- Traducción

## ICMPv6
Es la misma filosofía de [[ICMP]] adaptado para [[IPv6]].

![[Drawing 2024-01-30 16.32.09.excalidraw]]