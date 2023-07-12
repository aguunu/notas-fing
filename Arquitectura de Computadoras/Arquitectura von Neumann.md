Una *Arquitectura de von Neumann* tiene tres bloques constructivos básicos:
1. [[CPU|Central Process Unit]]
2. [[Memoria]]
3. [[Input & Output]]

![[Drawing 2023-07-08 17.19.51.excalidraw|center]]
## Bus
La conexión entre los sub-sistemas de [[CPU]], [[Memoria]] y [[Input & Output]], se realiza mediante *líneas de conexión* que comunican cierto tipo de información dependiendo el tipo de *bus*:
- Bus de Direcciones: Es formado por las *líneas de conexión* que transportan las direcciones de memoria o E/S a ser accedidas durante la transferencia
- Bus de Datos: Es formado por las *líneas de conexión* que transportan la información que es transferida sobre el bus entre los distintos componentes conectados
- Bus de Control: Es formado por las *líneas de conexión* que transportan señales que controlan el uso del bus y la comunicación sobre el mismo.

Por lo general, un *bus* esta definido por *especificaciones mecánicas, especificaciones eléctricas, protocolos de comunicación*.

Clasificación de *bus* según protocolos de comunicación*:
- Bus Simple: Este protocolo sigue la filosofía de *master-slave*, donde la entidad *master*  (usualmente la [[CPU]]) se encarga de controlar el *bus*, de esta forma, todas las transferencias son iniciadas, controladas y supervisadas por el *master*. Mientras que las entidades *slave* que desean utilizar el *bus* deben esperar a ser habilitadas por la entidad *master*.
- Bus Inteligente: Cualquier entidad tiene la capacidad de convertirse en *master* y comandar una transferencia. Observar que si varias entidades desean utilizar el bus, ocurre una "carreara" para decidir quién será el *master*. Por ende, según como se define el "ganador" en esta situación, surge la siguiente clasificación según el método de *arbitraje*:
	- Centralizado: El arbitraje se resuelve mediante una jerarquía; la entidad que tenga mayor jerarquía será la seleccionada. Las entidades utilizan *bus request* para hacer la petición al *bus* y reciben *bus grant* en caso de ser la elegida.
	- Distribuido: El arbitraje se resuelve mediante una especie de votación mediante todas las entidades conectadas al bus.

Clasificación de *bus* según aplicación:
Se define una "frontera" según la ubicación de las entidades a conectar.
- Internos: Un *bus* es interno si su función es conectar sub-sistemas dentro de la "frontera" del sistema *(ej. bus de memoria, que conecta la cpu con los bancos de memoria)*.
- Externos: Un *bus* es *externo* si su función es conectar sub-sistemas fuera de dicha frontera *(ej. bus USB, que se puede utilizar para conectar una amplia variedad de dispositivos externos)*.

### Bus de Expansión
Se utilizan para conectar placas de circuitos adicionales *(expansion cards/expansion boards)* a la placa de circuito principal del sistema *(motherboard)*.
