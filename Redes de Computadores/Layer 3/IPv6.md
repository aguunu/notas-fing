Existen 3 tipos de direcciones.
- *unicast:* la dirección representa una única interfaz.
	- *global unicast $\texttt{2000::/3}$:* son globalmente únicas y enrutables en internet. Su formato es $$\texttt{Global Routing Prefix (48-bits) | Subnet (16-bits) | Host (64-bits)}$$
	- *unique site local $\texttt{fc00::/7}$:* no son enrutables en internet. Por ende, son apropiadas por dispositivos que no tienen acceso a internet.
	- *link local $\texttt{fe80::/10}$:* son utilizadas para la comunicación de nodos en un mismo link local. Por ende, no son enrutables más halla del link.
- *multicast $\texttt{ff00::/8}$:* se utilizan para la comunicación de grupos dinámicos de nodos definiendo un *multicast group*.
- *anycast:* una misma dirección *anycast* puede ser asignada a varios nodos. No posee un prefijo especial, pues utiliza el mismo rango que *global unicast*.