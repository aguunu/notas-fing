Es una interfaz que permite la comunicación entre el [[CPU]] y el "mundo exterior exterior" mediante *input devices (ej. mouse y teclado)* y *output devices (ej. monitores e impresoras)*.

## Device Controller
Un __device controller__ es un componente que se encarga de operar sobre un *port*, *bus* o *device*. *(ej. el serial-port controller se encarga de controlar las señales en los cables del serial port)*.

El *device controller* posee ciertos *registros* que permiten la comunicación con el [[CPU]]. Por lo general, un *device controller* consiste de los siguientes registros:
- *data-in-register*: Contiene información destinada a la [[CPU]].
- *data-out register*: Contiene información proveniente de la [[CPU]].
- *status register*: Indica el estado del *device controller*.
- *control register*: Contiene información destinada al *device controller* para determinar que operación debe realizar.

Por otra parte, el *device controller* podría soportar __*memory-mapped I/O*__, de esta forma, se realiza un "mapeo" de estos registros al *address space* del procesador. Sin embargo, este "mapeo" a pesar de ser en memoria, puede tener comportamientos distintos según el tipo de registro:
- *Read Only*: El registro solo puede ser leído, en otro caso, la operación no tiene efecto.
- *Write Only*: Análogo a *Read Only*.
- *Independent Read/Write*: El *device controller* posee dos registros independientes, donde en uno se realizan las lecturas y en otro las escrituras.
- *Normal Read/Write*: Se comporta como una posición en memoria típica. 

La conexión entre el "computador" y un [[#Device Controller]] puede clasificarse según donde se encuentre el [[#Device Controller]].
- El [[#Device Controller]] reside en el "gabinete del computador":
	- El *device controller* se encuentra conectado directamente al bus interno del sistema.
	- El *device controller* conectado a un bus distinto al bus interno del sistema, el cual se conecta al bus interno a través de un adaptador.
- El *device controller* reside en el "gabinete del periférico".
	- Se utiliza una interfaz conectada directamente al bus interno del sistema.
	- Se utiliza un adaptador de bus conectado directamente al bus interno del sistema.
	- Se utiliza un adaptador de bus conectado a un bus distinto del bus interno.
- El *device controller* está distribuido entre el "gabinete del computador" y en el "gabinete del periférico".
