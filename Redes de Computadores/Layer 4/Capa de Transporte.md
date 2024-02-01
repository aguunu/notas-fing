Consiste en extender el servicio de comunicación host-to-host de la [[Capa de Red]], a un servicio de comunicación process-to-process para los servicios ejecutándose en los hosts encapsulando los datos en un *transport-layer segment*.

![[Drawing 2023-08-15 15.07.55.excalidraw|center]]

## Socket
Un *socket* es una manera de habilitar [[Inter Process Communication]] entre [[Procesos]] ejecutándose en un host, o en distintos hosts siguiendo el concepto de [[#Multiplexing]] y [[#Demultiplexing]].

## Multiplexing
El emisor se encargándose de administrar los datos que se envían por multiples [[#Socket]], encapsulándolos en un *transport layer segment* con los valores correspondientes.

## Demultiplexing
El receptor utiliza el *header* del *transport layer segment* para entregar los datos al [[#Socket]] correcto.

El host identifica el socket según su tipo para luego enviar el *payload* al socket identificado:
- Sin Conexión ([[UDP]]): el socket se identifica con los valores *(destination address, destination port)* del datagrama.
- Orientado a Conexión ([[TCP]]): el socket se identifica con los valores *(source address, source port, destination address, destination port)* del datagrama.


![[Drawing 2023-08-15 15.16.30.excalidraw|center]]

