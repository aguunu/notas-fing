## Batch System
Un *batch system* selecciona un subconjunto de *jobs (tareas)* de la *job pool* que se encuentra en memoria secundaria. Luego, el sistema ejecuta este subconjunto de *jobs* para un procesamiento más eficiente.

## Multiprogramming System
La *multiprogramación* consiste en incrementa el uso del CPU organizando los *jobs* para que de esta forma el CPU siempre tenga un *job* para ejecutar.

La idea es que el sistema operativo mantenga en memoria principal un subconjunto de *jobs* de la *job pool*. Luego, el sistema operativo elige uno de estos *jobs* y empieza su ejecución. Eventualmente el *job* podría esperar por alguna tarea *(ej. impresión de un documento)*. En un sistema sin multiprogramación, el CPU se mantendría *idle* esperando por la finalización de esta tarea. Sin embargo, en un *multiprogramming system*, se le otorgará el CPU a una tarea que este esperando por este.

>[!info] Ilusión de Paralelismo
>La técnica de *multiprogramación* produce una ilusión de *paralelismo*, haciéndole creer al usuario de que todos las *tareas* se ejecutan a la misma vez. Sin embargo, hay un único proceso ejecutándose en el procesador en un determinado instante.

## Time-Sharing System
Un *time-sharing system* o también conocido como *multi-tasking system*, es una extensión de los [[#Multiprogramming System]]. La técnica de *time-sharing* consiste en que el sistema operativo ejecute multiples tareas, intercambiándolas entre ellas *(CPU Scheduling)*. Este cambio es tan frecuente que el usuario no es capaz de notarlo, reduciendo así el *tiempo de respuesta*, lo que es ideal para *sistemas interactivos (ej. Windows)* donde varios usuarios son capaces de utilizar el sistema a la misma vez.

## Real Time System
El sistema esta sujeto al tiempo real, es decir, la respuesta del sistema debe estar garantizada en un tiempo definido o el sistema fallará.
- **Hard Real Time System**: El sistema nunca puede llegar a su *deadline* (fecha limite). De lo contrario, podrían producirse fallas irrecuperables en el sistema.
- **Soft Real Time System**: A diferencia del *Hard Real Time System*, si puede perder su *deadline* ocasionalmente.

## Multiprocessor System
También conocido como **Sistema Paralelo** y **Sistema Multicore**. Un *multiprocessor system* posee multiples procesadores que permiten la ejecución en [[Concurrencia#Paralelismo|Paralelo]] y sincronizada de varias tareas. Además, si un procesador falla, el sistema no se detiene ya que los demás siguen funcionando.

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
La **Taxonomía de Flynn** es una clasificación de arquitecturas de computadores en base a cuantos *flujos de instrucciones* y *flujos de datos* pueden ser procesados en simultaneo por dicha arquitectura.
- **Single Instruction Single Data (SISD)**: En una arquitectura SSID, existe un único procesador que ejecuta un único *flujo de instrucciones* y opera sobre un único *flujo de datos*. Es el tipo de arquitectura más simple y la más usada en los computadores tradicionales.
- **Single Instruction Multiple Data (SIMD)**: En una arquitectura SIMD , existe un único procesador que ejecuta la misma instrucción en multiples *flujos de datos* en simultaneo. Este tipo de arquitectura es usada en aplicaciones como procesamiento de imágenes y procesamiento de señales.
- **Multiple Instruction Single Data (MISD)**: En una arquitectura MISD, multiples procesadores ejecutan diferentes instrucciones en el mismo *flujo de datos*. Este tipo de arquitectura no es comúnmente usada en practica, pues difícilmente se encuentran aplicaciones que puedan ser descompuestas en *flujos de instrucciones* independientes.
- **Multiple Instruction Multiple Data (MIMD)**: En una arquitectura MIMD, multiples procesadores ejecutan diferentes instrucciones sobre diferentes *flujos de datos*. Este tipo de arquitectura es usada en tareas con alto nivel de computo *(ej. sistemas distribuidos y procesamiento paralelo).