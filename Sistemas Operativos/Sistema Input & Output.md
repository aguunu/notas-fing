El sistema operativo se encarga de administrar y controlar las operaciones I/O así como los dispositivos I/O.

## I/O Hardware
Un dispositivo se comunica a través de un *port (ej. serial port)*. Si los de dispositivos comparten un conjunto de cables, esta conexión es llamada *bus*.  

### Device Controller
Un __*device controller*__ es un componente que se encarga de operar sobre un *port*, *bus* o *device*. *(ej. el serial-port controller se encarga de controlar las señales en los cables del serial port)*.

El *device controller* posee registros dedicados a *datos* y *control de señales*, de esta forma, el procesador puede comunicarse con el *device controller* a través de estos registros. Por otro lado, el *device controller* podría soportar __*memory-mapped I/O*__, de esta forma, mapeando los registros de este dentro del *address space* del procesador.

Por lo general, un *device controller* consiste de 4 registros:
- *data-in-register*
- *data-out register*
- *status register*
- *control register*

### Handshaking
El *handshaking* es la comunicación entre el sistema operativo *(host)* y el *device controller*.

#### Programmed I/O
La técnica de __*programmed I/O*__ consiste en realizar una solicitud al dispositivo y esperar a que se realice mediante [[Sección Crítica#Busy Waiting|Polling]]. Una vez realizada, el proceso saldrá del bucle y finalmente podrá leer el registro del *controller*.

```c
// realizar solicitud
// ...
while (device_status_register != READY); // busy waiting
// usar dispositivo 
// ...
```

>[!warning] 
>Para dispositivos que transfieren grandes cantidades de datos, esta solución no es eficiente. Pues, los registros suelen tener un tamaño pequeño.

#### Interrupt-Driven I/O
Cuando un proceso $p_0$ hace realiza una operación IO, la técnica de __*Interrupt-Driven I/O*__ consiste de los siguientes pasos:
1. $p_0$ se agrega a una cola de espera asociada al dispositivo y es bloqueado por el [[Scheduling]].
2. Una vez que el dispositivo completa la tarea, genera una interrupción *(el estado del CPU es guardado en el stack)*.
3. El CPU recibe la interrupción y transfiere el control al *interrupt handler*.
4. El *interrupt handler* se encarga de procesar los datos. Luego retorna de la interrupción cargando el estado anterior a la interrupción del CPU y desbloqueando a $p_0$ mediante [[Scheduling]].

>[!success] 
>El método de *interrupt-driven I/O* tiene la ventaja de que cuando un proceso se bloquea al hacer una operación IO, el CPU podrá ser usado por otro proceso mediante [[Scheduling]].

>[!warning] 
>Observar que el sistema se degrada debido a los procesos que constantemente realizan operaciones IO. Pues, constantemente se están generando interrupciones.

#### Direct Memory Access
La técnica de __*direct memory access (DMA)*__ consiste en cargar ciertos registros del *device controller* en el __*DMA Controller*__. De esta forma, el *DMA Controller* se encarga de la transferencia, interrumpiendo al procesador cuando esta finalice.

## Interfaz de Sistema Entrada & Salida
El objetivo es independizar el sistema de I/O del hardware. De esta forma, simplificando el trabajo para los desarrolladores.

### Clasificación de Dispositivos
- Block Devices: Dispositivos donde su granularidad de información es a nivel de bloques.
- Char Devices: Dispositivos donde su granularidad es a través de caracteres.

### Clasificación de Operaciones
- Blocking: Cuando un proceso requiere de un servicio de I/O a través de una rutina bloqueante, el proceso se suspende hasta que la operación haya finalizado.
- Nonblocking: El llamado al servicio de I/O es devuelto tan pronto como sea posible.
- Asynchronous: La operación es ejecutada en paralelo. Cuando finaliza le avisa a través de una señal.
- Synchronous: Los procesos que realizan pedidos de I/O se bloquean hasta que el pedido finalice.

## Subsistema de Input & Output
El kernel brinda varios servicios para el manejo de operaciones I/O.

### I/O Scheduling
La técnica de *I/O Scheduling* se apoya sobre la planificación para lograr un buen rendimiento del dispositivo.

Cuando un proceso se bloquea al realizar una operación I/O, es puesto en la cola del dispositivo correspondiente y el subsistema de I/O reorganiza los pedidos para lograr un mayor rendimiento.

### Buffering
El *buggering* es un lugar de memoria que guarda datos mientras son transferidos entre dos dispositivos o un dispositivo y una aplicación.

### Caching
La utilidad del *caching* es acelerar el acceso a la información.

### Spooling
La técnica de *spooling* consiste en un buffer que mantiene salida para un dispositivo que no se pueda intercalar *(ej. los datos de la cola de impresión de una impresora)*.

### Error Handling
Cada llamado a sistema retorna un bit que informa el éxito o fracaso de una operación I/O.

>[!info] 
>En UNIX se utiliza una variable `errno` que es utilizada para codificar el error.