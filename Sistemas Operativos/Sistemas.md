## Batch System (lotes).
El sistema selecciona un subconjunto de *jobs (tareas)* de la *job pool* que se encuentra en memoria secundaria. Luego, el sistema ejecuta este subconjunto de *jobs* para un procesamiento más eficiente.

### Batch System con Multiprogramación
Es una variante al *Batch System*, donde se utiliza la técnica de [[#Multiprogramación]] sobre el conjunto de tareas que se encuentra cargado en memoria principal.

## Time-Sharing System
Permite a varios usuarios compartir el CPU simultáneamente, utilizando técnicas de [[#Multi-Tasking]] y [[#Multiprogramación]]. Estas técnicas permiten que los usuarios que estén haciendo uso del sistema no sean capaces de notar que hay más usuarios usando el mismo sistema.

## Real Time System
El sistema esta sujeto al tiempo real, es decir, la respuesta del sistema debe estar garantizada en un tiempo definido o el sistema fallará.
- **Hard Real Time System**: El sistema nunca puede llegar a su *deadline* (fecha limite). De lo contrario, podrían producirse fallas irrecuperables en el sistema.
- **Soft Real Time System**: A diferencia del *Hard Real Time System*, si puede perder su *deadline* ocasionalmente.

## Sistema Multiprocesador (Paralelos)
Tambien conocido como **Sistema Paralelo** y **Sistema Multicore**. El sistema posee multiples procesadores que permiten la ejecución simultanea y sincronizada de varios *jobs (tareas)*.
Si un procesador falla, el sistema no se detiene ya que los demás siguen funcionando.

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
***
## Multiprogramación
Cuando un *job (tarea)* que esta en ejecución espera por otra tarea externa al CPU *(ej. impresión de un documento)*, el sistema le otorga el CPU a otro *job* *(mediante algoritmos de CPU Scheduling)* y de esta forma reducir el tiempo muerto del CPU.

## Multi-Tasking
El CPU ejecuta concurrentemente multiple *jobs* intercambiándolos entre ellos haciendo uso de *algoritmos de CPU Scheduling*.
