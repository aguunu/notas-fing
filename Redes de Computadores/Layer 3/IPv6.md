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
Las direcciones especiales en IPv6 son las siguientes:
- *($\texttt{::/128}$) unspecified address*
- *($\texttt{::1/128}$) loopback address*
- *($\texttt{::/0}$) default route*

Además el protocolo IPv6 ==no define una dirección de tipo broadcast==. Las direcciones se pueden clasificar según su funcionalidad.

### Unicast Address
Una *unicast address* identifica una única interfaz.
- *global unicast $\texttt{2000::/3}$:* son globalmente únicas y enrutables en internet. Su formato es $$\texttt{Global Routing Prefix (48-bits) | Subnet (16-bits) | Host (64-bits)}$$
- *unique site local $\texttt{fc00::/7}$:* no son enrutables en internet. Por ende, son apropiadas por dispositivos que no tienen acceso a internet.
- *link local $\texttt{fe80::/10}$:* son utilizadas para la comunicación de nodos en un mismo link local. Por ende, no son enrutables más halla del link.

### Multicas Address
Una *multicast address* identifica a un grupo de interfaces. Un paquete cuyo destino es una dirección *multicast* es entregado a todos los nodos del *multicast group*. *Notar: utilizan el prefijo $\texttt{ff00::/8}$*

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