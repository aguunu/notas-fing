El protocolo ARP *(Address Resolution Protocol)* es un protocolo de [[Capa de Enlace]] utilizado para mapear direcciones de [[Capa de Red]] ([[IP Address]]) a direcciones de [[Capa de Enlace]] ([[MAC Address]]).

Cuando un dispositivo en una red necesita comunicarse con otro dispositivo en la misma red, utiliza direcciones IP para identificar los destinos. Sin embargo, para enviar datos a través del medio físico, como cables Ethernet, se requiere la dirección MAC del dispositivo de destino.

El proceso de resolución de direcciones ARP se realiza de la siguiente manera:
1. **ARP Request:** El dispositivo emisor conoce la dirección IP del dispositivo de destino, pero no su dirección MAC. Envía una solicitud ARP a la dirección MAC broadcast ($\texttt{FF-FF-FF-FF-FF-FF}$) preguntando: *"¿Quién tiene esta dirección IP?"*. Por lo que cada dispositivo en la LAN recibe esta ARP request.
2. **ARP Reply:** El dispositivo de destino, que tiene la dirección IP mencionada, responde con su dirección MAC. Esto completa la tabla ARP en el dispositivo emisor, asociando la dirección IP con la dirección MAC correspondiente.
3. **Tabla ARP (ARP Cache):** Después de obtener la respuesta, el dispositivo emisor almacena la información $\texttt{(IP addr, MAC addr, TTL)}$ en su tabla ARP  manteniéndola hasta que expire el $\texttt{TTL}$.