==Es un dispositivo [[Enlace#Duplex|Full-Duplex]] de [[Capa de Enlace]] cuyo objetivo es reenviar [[Ethernet#Ethernet Frame|Frames]], examinando su [[MAC Address]]. Además, logra crear un [[Capa de Enlace#Dominio de Colisión|Dominio de Colisión]] distinto por cada uno de sus [[Enlace|Enlaces]]==.

>[!warning] 
>Un *switch* no posee [[MAC Address]] ni tampoco [[IP Address]]. Además, un *switch* es *invisible* para todos los nodos de la red.

## Auto Aprendizaje
El *switch* "aprende" que *hosts* pueden ser alcanzados mediante sus interfaces. Para esto, cuando un [[Ethernet#Ethernet Frame|Frame]] es recibido, el *switch* "aprende" la ubicación del emisor almacenando $\texttt{(MAC addr, interface, TTL)}$ en la *switch table*. Además, si al momento de recibir un *frame*, la [[MAC Address]] destino no se encuentra en la *switch table*, el *frame* es retransmitido a todas las interfaces.
