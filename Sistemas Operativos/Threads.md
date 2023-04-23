Cada proceso puede tener multiples threads (*multithreaded*) que *"viven"* en el [[Procesos#Process Control Block (PCB)|PCB]] de dicho proceso. Por ende, el código, archivos e información es compartida entre ellos. Sin embargo, cada *thread* tiene su propio set de registros (incluye program counter) y stack.

*Observación: hasta el momento estuvimos trabajando con procesos **single-threaded**, es decir, procesos con un solo thread.*

*Observación: crear un proceso es más costoso que crear un thread, pues para crear un proceso se necesita reservar memoria y recursos.*

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
- **Aprovechamiento de un [[Sistemas#Sistema Multiprocesador (Paralelos)|Sistema Multiprocesador]]**: El SO puede asignar threads de un proceso en diferentes procesadores.
- **Independencia**: Al ejecutarse los threads de forma independiente, si un thread se bloquea, los demás pueden seguir en ejecución.

### Modelos
- *Many To One*: $n$ threads a nivel de usuario corresponden a un thread a nivel de kernel.
- *One To One*: Un thread a nivel de usuarios corresponde a un único thread a nivel de kernel.
- *Many To Many*: $n$ threads a nivel de usuario corresponden a $m$ threads a nivel de kernel.
