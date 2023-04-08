## Sistema Operativo
Es un programa que controla el *hardware*. Funciona como una interfaz entre el usuario y el hardware, escondiendo así detalles sobre la arquitectura en la que se esta trabajando.

### Objetivos
Los sistemas operativos tienen diferentes objetivos dependiendo su fin, por ejemplo, los sistemas operativos para servidores se destacan por la optimización del hardware. En cambio, sistemas operativos usados en smartphones proveen una interfaz para que el usuario pueda interactuar fácilmente con el software.
Por ende, algunos sistemas están centrados en la *eficiencia* y otros en la *conveniencia* del mismo.

### Funcionalidades
Las principales funcionalidades de un sistema operativos son las siguientes:
- Interfaz para el usuario
- Ejecución de programas
- Operaciones de IO
- Manipular el *File System*
- Comunicaciones
- Administrar recursos
- Protección & Seguridad

### System Batch (lotes).
Los *jobs (tareas)* se agrupan en conjuntos para un procesamiento más eficiente.

### Sistema Batch con Multiprogramación 
El sistema selecciona un subconjunto de la *job pool* que está en memoria secundaria para ser cargado en memoria principal.
Luego, el sistema ejecuta un *job* de este subconjunto, mientras el *job* que esta en ejecución espera por otra tarea (*ej. impresión de un documento*), el sistema elige otro *job* para que haga uso del CPU (*multiprogramación*), reduciendo así el tiempo muerto del CPU.

### Time-Sharing System
Permite a los usuarios compartir el CPU simultáneamente, utilizando *CPU Scheduling* y *multiprogramación*.
- Multi-tasking *(Time Sharing)*: El CPU ejecuta multiple *jobs* intercambiándolos entre ellos *(algoritmos de CPU Scheduling)*. Este cambio es tan frecuente que el usuario no es capaz de notarlo.

### Computadoras Personales
El sistema operativa maximiza la interacción con el usuario, en vez del uso del CPU.

### Sistema Multiprocesador (Paralelos)

^6c7002

Tambien conocido como **Sistema Paralelo** y **Sistema Multicore**. El sistema posee multiples procesadores que permiten la ejecución simultanea y sincronizada de varios procesos.
Si un procesador falla, el sistema no se detiene ya que los demás siguen funcionando.

1. UMA *(Uniform Memory Access)*: Cada procesador accede a cualquier lugar de memoria, con el mismo costo de tiempo.
2. NUMA *(Non Uniform Memory Access)*: Los procesadores tienen conjuntos de memoria a la cual acceden más rápido que el resto.

#### Clasificación
1. Según como se ejecutan
	- **Symmetric Multiprocessing**: Los procesadores trabajan como si fueran un único procesador, realizando todo el trabajo.
	- **Asymmetric Multiprocessing**: Existe un *procesador maestro* que planifica y asigna el trabajo de los otros procesadores *(slaves)*.
2. Según como se comunican
	- **Altamente integrados**: Los canales de comunicación son rápidos, a través de un bus común.
	- **Levemente integrados**: Los canales son lentos, a través de una red.
3. Según el uso de memoria
	- **Sistemas de Memoria Compartida**: Los procesadores se encuentran en un único nodo altamente integrado, todos comparten el bus que los conecta a memoria
	- **Sistema de Memoria Distribuida**: Los procesadores tienen su propia memoria y están conectados a través de redes.

### Taxonomía de Flynn
La **Taxonomía de Flynn** es una clasificación de arquitectura de computadores en función de cuantas instrucciones se ejecutan al simultaneo y sobre que datos.
- SISD *(Single Instruction, Single Data)*: una arquitectura secuencial donde no existe paralelismo (sistemas monoprocesadores).
- SIMD *(Single Instruction, Multiple Data)*: sistemas que ejecutan la misma instrucción sobre un conjunto distinto de datos (sistemas vectoriales).
- MISD *(Multiple Instruction, Single Data)*: utilizado para paralelismo redundante.
- MIMD *(Multiple Instruction, Multiple Data)*: sistemas con procesadores autónomos que ejecutan en forma simultánea diferentes instrucciones sobre diferentes datos.

### Real Time System
El sistema esta sujeto al tiempo real, la respuesta del sistema debe estar garantizada en un tiempo definido o el sistema fallará.
- **Hard Real Time System**: El sistema nunca puede llegar a su *deadline* (fecha limite). De lo contrario, podrían producirse fallas irrecuperables en el sistema.
- **Soft Real Time System**: A diferencia del *Hard Real Time System*, si puede perder su *deadline* ocasionalmente.