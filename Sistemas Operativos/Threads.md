Todo [[Procesos|Proceso]] tiene al menos un thread *(main thread)*. Un proceso que solo contiene su *main-thread* se le conoce como **single-thread process**. Por otro lado, un proceso con multiples *threads* se le denomina **multithreaded process**. Además, cada *thread* se ubica en el [[Procesos#Process Control Block (PCB)|PCB]] correspondiente a su proceso.

## Disposición en Memoria
Un *thread* en memoria se puede descomponer de la siguiente forma:
- **Program Counter**
- **Set de Registros**
- **Stack**

Además, comparte con otros threads pertenecientes al mismo proceso los siguientes _ _:
- **Code segment**
- **Data segment**
- **Heap**
- **Recursos del sistema operativo** *(ej. archivos)*.

>[!bug] Memory Address Space
>A diferencia de los [[Procesos]], los *threads* de un proceso comparten la misma *memory address space* de dicho proceso. Por consecuencia, un *thread* con un mal comportamiento podría afectar a todo el proceso.

>[!success] Performance
>Crear un proceso es más costoso que crear un thread, pues para crear un proceso se necesita reservar memoria y recursos.

## Implementación
Los *threads* pueden implementarse tanto a *nivel de usuario* como a *nivel de kernel*.
- **User Threads**: El usuario implementa una librería *(thread library)* que provee soporte para crear, planificar y administrar los *threads*. *(El sistema operativo reconocerá el proceso como **single-threaded** sin importar la cantidad de threads que este posea).*
- **Kernel Threads**: El sistema operativo provee el soporte para crear, planificar y administrar los *threads*.

### Ventajas de *User Threads*
- **Portabilidad**: Se puede portar la librería a otros sistemas operativos que no tengan soporte para threads.
- **[[Scheduling]] Personalizable**: Se puede crear estrategias diferentes a las que utiliza el SO. 
- **[[Procesos#Context Switch|Context Switch]]**: El *[[Procesos#Context Switch|Context Switch]]* entre threads será más simple.

*Observación: por lo general serán más rápidos que los kernel threads, pues no requiere que el SO intervenga (system calls, context switch, scheduling, etc).*

### Ventajas de *Kernel Threads*
- **Aprovechamiento de un [[Sistemas#Multiprocessor System|Multiprocessor System]]**: El SO puede asignar threads de un proceso en diferentes procesadores.
- **Independencia**: Al ejecutarse los threads de forma independiente, si un thread se bloquea, los demás pueden seguir en ejecución.

### Modelos
- *Many To One*: $n$ threads a nivel de usuario corresponden a un thread a nivel de kernel.
- *One To One*: Un thread a nivel de usuarios corresponde a un único thread a nivel de kernel.
- *Many To Many*: $n$ threads a nivel de usuario corresponden a $m$ threads a nivel de kernel.

>[!bug] Bloqueo de Threads
>En un modelo *Many To One*, al bloquearse un thread a nivel de usuario correspondiente a un thread a nivel de kernel $t$, se bloquearan todos los threads a nivel de usuario que correspondan a $t$.
