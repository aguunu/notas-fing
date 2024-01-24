Es un estándar de red utilizado para la transmisión de datos en *Local Area Networks (LANs)*. Utiliza [[Multiple Access Protocols#CSMA/CD|CSMA/CD]] para gestionar el acceso compartido al canal de comunicación.

- Bus Physical Topology: todos los nodos se encuentran en el mismo dominio de colisión.
- Star Physical Topology: existe un *switch* activo en el centro haciendo que los nodos no colisionen entre ellos.

## Ethernet Frame
El datagrama correspondiente al protocolo de red *(ej. IPv4)* es encapsulado en un *Ethernet frame*.

- *Preamble (8 bytes):* un patron de 7 bytes 10101010 seguido del byte 10101011 usado para sincronizar el *clock* del emisor y receptor.
- *Destination address (6 bytes)*: [[MAC Address]] destino, si el valor de este campo coincide con la [[MAC Address]] de la interfaz o se trata de la dirección MAC broadcast, se procesa el *frame*. En otro caso, la interfaz descarta el *frame*.
- *Source address (6 bytes):* [[MAC Address]] origen.
- *Type (2 bytes):* indica el protocolo de capa superior.
- *payload (46-1500 bytes):* los datos del datagrama de la capa superior. *Notar que el MTU máximo es de 1500 bytes.*
- *CRC (4 bytes):* campo de verificación de [[Capa de Enlace#Cyclic Redundancy Check (CRC)|CRC]]. Si se detecta un error, el *frame* se descarta.

>[!info] 
>Observar que un *ethernet frame* tendrá un tamaño mínimo de 64 bytes y un tamaño máximo de 1518 bytes.

## Ethernet Switch
Su objetivo es almacenar y retransmitir *ethernet frames*, examinando la [[MAC Address]] del *frame* entrante.

>[!warning] 
>Un *switch* no posee [[MAC Address]] ni tampoco [[IP Address]]. Además, un *switch* es invisible para todos los nodos de la red.

### Auto Aprendizaje
El *switch* "aprende" que *hosts* pueden ser alcanzados mediante sus interfaces. Para esto, cuando un *frame* es recibido el *switch* "aprende" la ubicación del emisor almacenando $\texttt{(MAC addr, interface, TTL)}$ en la *switch table*.
Al momento de recibir un *frame*, si la [[MAC Address]] destino no se encuentra en la *switch table*, el *frame* es retransmitido a todas las interfaces.

### VLAN
Un *switch* que soporta VLAN puede ser configurado para definir multiples *virtual* LANs sobre una única LAN.

#### Port-Based VLAN
Los puertos del switch se agrupan, de esta forma, un único switch opera como multiples *switches virtuales*.

- *Traffic Isolation:* Los *frames* provenientes de un grupo solo pueden alcanzar puertos dentro de ese grupo.
- *Dynamic Membership:* Los puertos pueden ser dinámicamente asignados entre las VLANs.
- *Forwarding between VLANs:* Se logra mediante enrutamiento.
- *Trunk Port:* Transmite *frames* entre VLANs definidas en multiples *physical switches*. Los *frames* transmitidos entre VLANs no pueden ser 802.1 *frames* ya que deben tener información sobre la identificación de la VLAN. Por ende, surge el protocolo *802.1q* que agrega y elimina campos a los *frames* que pasan entre puertos *trunk*, además de recalcular el campo CRC.
	- *Tag Protocol Identifier (2 bytes)*
	- *Tag Control Information (12 bits)*
	- *Priority (3 bits)*
