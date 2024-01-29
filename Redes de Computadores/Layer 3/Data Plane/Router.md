## Switching Fabric
Se encarga de transferir el paquete desde el buffer de entrada al buffer de salida correspondiente.

- Switching por Memoria: el paquete es copiado a la memoria del sistema. Por ende, la velocidad está limitada por el ancho de banda de la memoria.
- Switching por Bus: el paquete va desde la memoria del puerto de entrada a la memoria del puerto de salida mediante un bus compartido. Por ende, la velocidad estará limitada por el ancho de banda del bus. Además, un solo paquete podrá estar siendo procesado en simultaneo. Un paquete que llega y encuentra el bus ocupado, es puesto en la cola de espera asociada al puerto de entrada.
- Switching por Crossbar: Supera las limitaciones de *switching por bus*.

![[Drawing 2023-11-19 17.13.13.excalidraw|center]]

Un paquete que se encuentra bloqueado puede impedirle el paso a paquetes que arriban en la misma interfaz, de esta forma, bloqueándolos. A este evento se le denomina **Head-of-the-Line (HOL)**.
Por otra parte, los paquetes que arriban en determinada interfaz pueden ser descartados en caso de que el *buffer* de dicha interfaz se encuentre lleno.

## Packet Scheduling
Se encarga de seleccionar el próximo paquete a enviar por el enlace.
- FIFO Scheduling: Se envían en orden de arribo.
	- *discard policy:* *tail drop, priority, random.*
- Priority Scheduling: Se envían según prioridad. *La prioridad puede ser en base a dirección origen/destino, puerto origen/destino, etc.*
- Round Robin (RR): Cíclicamente escanea las colas de las clases, enviando un paquete de cada clase.
- Weighted Fair Queuing (WFQ): Una modificación de *Round Robin*, asignándole un peso a cada clase.
