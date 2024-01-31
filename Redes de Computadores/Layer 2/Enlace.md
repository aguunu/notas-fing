## Enlace Point To Point
Un enlace *point-to-point (PPP)* consiste de un único nodo emisor en uno de los extremos del enlace, y un único nodo receptor en el extremo opuesto.

Algunos ejemplos:
 - Twisted Pair (TP)
 - Coaxial Cable
 - Fiber Optic Cable

## Enlace Broadcast
En un enlace *broadcast*, más de dos nodos pueden estar conectados, ya sea compartiendo un medio en común (*shared-medium*).

Algunos ejemplos:
- Wireless Radio: La señales se comunican a través de bandas que se encuentran en el *espectro electromagnético*.
		- 802.11 WLAN (Wireless Local Access Network)
		- Wide-Area *(e.g. 4G)*
		- Bluetooth
		- Terrestrial Microwave
		- Satellite 

>[!warning]
>En este tipo de enlace, puede ocurrir interferencia (colision) cuando dos o más nodos intentan utilizar el *shared-medium* en simultaneo. Por esta razón se utilizan [[Multiple Access Protocols]] que se encargan de solucionar este problema.

## Duplex
Los enlaces pueden ser clasificados según el *duplex* de la comunicación:
![[Drawing 2023-09-20 11.08.41.excalidraw|center]]
