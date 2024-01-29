Existen 3 tipos de direcciones.
- *unicast:* la dirección representa una única interfaz.
	- *global unicast $\texttt{2000::/3}$:* son globalmente únicas y enrutables en internet. Su formato es $$\texttt{Global Routing Prefix (48-bits) | Subnet (16-bits) | Host (64-bits)}$$
	- *unique site local $\texttt{fc00::/7}$:* no son enrutables en internet. Por ende, son apropiadas por dispositivos que no tienen acceso a internet.
	- *link local $\texttt{fe80::/10}$:* son utilizadas para la comunicación de nodos en un mismo link local. Por ende, no son enrutables más halla del link.
- *multicast $\texttt{ff00::/8}$:* se utilizan para la comunicación de grupos dinámicos de nodos definiendo un *multicast group*.
- *anycast:* una misma dirección *anycast* puede ser asignada a varios nodos. No posee un prefijo especial, pues utiliza el mismo rango que *global unicast*.

Notar: No se especifica una dirección de broadcast para IPv6.


![[Drawing 2024-01-28 15.53.38.excalidraw|center]]

## Fragmentación
IPv6 ==no soporta fragmentación==. Cualquier enlace que soporte IPv6 debe ser capaz de soportar un [[Maximum Transmission Unit|MTU]] de al menos 1280 bytes. Por ende, si un nodo desea enviar paquetes mayores a 1280 bytes, este debe determinar el MTU mínimo admitido a lo largo de la ruta entre el origen y el destino mediante *Path MTU*. En caso de ser necesario, el nodo origen es el encargado de fragmentar el paquete para poder ser enviado por la ruta.

*Notar: el IPv6 header no contiene información sobre posible fragmentación. En caso de fragmentación, se utiliza un __fragmentation header__ que contiene la información y se asocia en el campo __next header__.*