*Dynamic Host Configuration Protocol (DHCP)* permite a los hosts obtener una dirección IP de forma automática cuando estos se unen a la red. Además, DHCP permite conocer información adicional de la red como la dirección del *gateway* o servidor [[DNS]] de la red.

Se definen 4 tipos de mensajes en el protocolo DHCP que se envían sobre [[UDP]]:
1. $\texttt{DHCP discover}$: El cliente envía un mensaje $\texttt{DCHP discover}$ al puerto 67, a la dirección de broadcast 255.255.255.255.
2. $\texttt{DHCP offer}$: El servidor DHCP recibe el mensaje $\texttt{DHCP discover}$ y responde al cliente mediante un mensaje $\texttt{DHCP offer}$, nuevamente con destino broadcast, ya que el cliente aún no tiene dirección IP asignada.
3. $\texttt{DHCP request}$: El nuevo cliente elige una entre varios *server-offers*, y responde a este con un mensaje $\texttt{DHCP request}$.
4. $\texttt{DHCP ACK}$. El servidor confirma el $\texttt{DHCP request}$ con un $\texttt{DHCP ACK}$, confirmando los parámetros solicitados.

![[Drawing 2023-11-19 18.30.49.excalidraw|center]]