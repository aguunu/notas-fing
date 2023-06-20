Un *disco* contiene un ***spindle***, que sostiene y hace rotar un conjunto de platos magnéticos denominados ***platters***.

Cada *platter* es dividido en un número de anillos, donde cada uno de estos es conocido como ***track***. El conjunto de todos los *tracks* de un *disco* que están a la misma distancia del *spindle*, es conocido como ***cylinder***. Además, cada *platter* posee su **read-write head** para manipular la información sobre este. Cada *read-write head* esta unida a su propio **read-write arm** también conocido como ***actuator***. Todos los *read-write arms* están sujetos a un brazo en común denominado ***assembly arm***.

Los *tracks* se dividen en ***sectors*** de tamaño fijo que representa la unidad básica de almacenamiento en disco *(ej. sectors de 512 bytes)*. *Observar que los tracks de la periferia tendrán más sectors que los tracks más cercanos al spindle*. Luego, los *sectors* son agrupados en ***clusters***, que representan la unidad mínima de almacenamiento en disco.

## Disk Scheduling
El sistema operativo es responsable de usar el hardware de forma eficiente. Para los *discos*, esto es, tener un rápido *disk time access* y lograr tener un gran *ancho de banda*.
El *disk time access* tiene dos grandes componentes:
1. Seek Time: Tiempo en el que el *read-write arm* posiciona su *read-write head* en el *cylinder* correspondiente al *sector* deseado.
2. Rotational Latency: Tiempo en que demora el disco en rotar al sector deseado.
Definiéndolo de la siguiente manera:
- ***disk time access = seek time + rotational latency + transfer time***

Por otro lado, definimos el *ancho de banda* de una transferencia, como:
- ***bandwidth = total bytes / (last transfer time - first request time)***

### First Come, First Serve
El algoritmo *first come first serve (FCFS)* sigue el principio FIFO, es decir, la primer solicitud que llega, es la primer solicitud que se atiende.

>[!success] 
>A pesar de que no es una solución óptima para *hard drives*, si lo es para *solid state drives*, ya que estos últimos no tienen partes mecanicas.


### Shortest Seek Time First
El algoritmo *shortest seek time first (SSTF)*, selecciona la solicitud con menor *Seek Time*.

>[!warning] 
>El caso donde llegan solicitudes constantemente sobre cierto *track*, causa que las solicitudes sobre otros *tracks* no sean atendidas.

### SCAN
El algoritmo *SCAN*, recorre el conjunto de *tracks* del disco desde el centro a la periferia, atendiendo las solicitudes que va encontrando. Al llegar al final, realiza el recorrido inverso.

### C-SCAN
El algoritmo *C-SCAN*, es una modificación del algoritmo [[#SCAN]]. Cuando este llega al final del recorrido, vuelve al inicio y empieza nuevamente el recorrido.

### LOOK
El algoritmo *LOOK*, es una modificación del algoritmo [[#SCAN]]. Iniciando el recorrido en la primera solicitud y finalizando en la última.

### C-LOOK
El algoritmo *C-LOOK*, es una combinación de los algoritmos [[#C-SCAN]] y [[#LOOK]]. Inicia el recorrido en la primera solicitud y finaliza en la última. Luego se vuelve a la primera solicitud y se inicia nuevamente el recorrido.

## Manejo de Discos
Antes de que un disco puede almacenar información, deberá ser dividido en sectores que luego el controlador usará para lectura/escritura. Este proceso se llama *low-level formatting* o *physical formatting*. Luego, la estructura de un sector tendrá, típicamente, un bloque de 512 bytes, e información usada por el controlador *(ej. número de sector, error-correcting code ECC)*.

Luego, para poder ser usado, el sistema operativo primero particionará el disco en una o varias particiones para luego crear un [[File System]] sobre la partición *(logical formatting)*. De esta forma, almacenando la estructura del *file system* en dicha partición.

>[!info] 
>El sistema operativo puede darle la habilidad a ciertas aplicaciones de usar particiones que no posean *logical formatting* llamadas *(RAW disk/unformatted disk)*. Por ejemplo, algunas bases de datos prefieren este método ya que podrán tener control exacto sobre las posiciones en el disco.

## Boot Block
TODO
