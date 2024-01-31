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
- *CRC (4 bytes):* campo de verificación de [[Detección y Corrección de Errores#Cyclic Redundancy Check|CRC]]. Si se detecta un error, el *frame* se descarta.

>[!info] 
>Observar que un *ethernet frame* tendrá un tamaño mínimo de 64 bytes y un tamaño máximo de 1518 bytes.
