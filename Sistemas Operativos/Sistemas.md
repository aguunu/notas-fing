## Batch System (lotes).
El sistema selecciona un subconjunto de *jobs (tareas)* de la *job pool* que se encuentra en memoria secundaria. Luego, el sistema ejecuta este subconjunto de *jobs* para un procesamiento más eficiente.

## Multiprogramming System
La *multiprogramación* es una técnica que incrementa el uso del CPU organizando los *jobs* para que de esta forma el CPU siempre tenga un *job* para ejecutar.

La idea es que el sistema operativo mantenga en memoria principal un subconjunto de *jobs* de la *job pool*. Luego, el sistema operativo elige uno de estos *jobs* y empieza su ejecución. Eventualmente el *job* podría esperar por alguna tarea *(ej. impresión de un documento)*. En un sistema sin multiprogramación, el CPU se mantendría *idle* esperando por la finalización de esta tarea. Sin embargo, en un sistema con multiprogramación, se le otorgará el CPU a una tarea que este esperando por este.

>[!info] Ilusión de Paralelismo
>La técnica de *multiprogramación* produce una ilusión de *paralelismo*, haciéndole creer al usuario de que todos las *tareas* se ejecutan a la misma vez. Sin embargo, hay un único proceso ejecutándose en el procesador en un determinado instante.

## Time-Sharing (Multi-Tasking) System
Es una extensión de los [[#Multiprogramming System]]. La técnica de *time-sharing* consiste en que el sistema operativo ejecute multiples tareas, intercambiándolas entre ellas *(CPU Scheduling)*. Este cambio es tan frecuente que el usuario no es capaz de notarlo, reduciendo así el *tiempo de respuesta*, lo que es ideal para *sistemas interactivos (ej. Windows)* donde varios usuarios son capaces de utilizar el sistema a la misma vez.

## Real Time System
El sistema esta sujeto al tiempo real, es decir, la respuesta del sistema debe estar garantizada en un tiempo definido o el sistema fallará.
- **Hard Real Time System**: El sistema nunca puede llegar a su *deadline* (fecha limite). De lo contrario, podrían producirse fallas irrecuperables en el sistema.
- **Soft Real Time System**: A diferencia del *Hard Real Time System*, si puede perder su *deadline* ocasionalmente.

## Multiprocessor System
Tambien conocido como **Sistema Paralelo** y **Sistema Multicore**. Un *multiprocessor system* posee multiples procesadores que permiten la ejecución en [[Concurrencia#Paralelismo|Paralelo]] y sincronizada de varias tareas. Además, si un procesador falla, el sistema no se detiene ya que los demás siguen funcionando.

1. UMA *(Uniform Memory Access)*: Cada procesador accede a cualquier lugar de memoria, con el mismo costo de tiempo.
2. NUMA *(Non Uniform Memory Access)*: Los procesadores tienen conjuntos de memoria a la cual acceden más rápido que el resto.

### Clasificación
1. Según como se ejecutan
	- **Symmetric Multiprocessing**: Los procesadores trabajan como si fueran un único procesador, realizando todo el trabajo.
	- **Asymmetric Multiprocessing**: Existe un *procesador maestro* que planifica y asigna el trabajo de los otros procesadores *(slaves)*.
2. Según como se comunican
	- **Altamente integrados**: Los canales de comunicación son rápidos, a través de un bus común.
	- **Levemente integrados**: Los canales son lentos, a través de una red.
3. Según el uso de memoria
	- **Sistemas de Memoria Compartida**: Los procesadores se encuentran en un único nodo altamente integrado, todos comparten el bus que los conecta a memoria
	- **Sistema de Memoria Distribuida**: Los procesadores tienen su propia memoria y están conectados a través de redes.

## Taxonomía de Flynn
La **Taxonomía de Flynn** es una clasificación de arquitectura de computadores en función de cuantas instrucciones se ejecutan al simultaneo y sobre que datos.
- SISD *(Single Instruction, Single Data)*: una arquitectura secuencial donde no existe paralelismo (sistemas monoprocesadores).
- SIMD *(Single Instruction, Multiple Data)*: sistemas que ejecutan la misma instrucción sobre un conjunto distinto de datos (sistemas vectoriales).
- MISD *(Multiple Instruction, Single Data)*: utilizado para paralelismo redundante.
- MIMD *(Multiple Instruction, Multiple Data)*: sistemas con procesadores autónomos que ejecutan en forma simultánea diferentes instrucciones sobre diferentes datos.
