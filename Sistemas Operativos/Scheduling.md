Es la base para lograr la [[Sistemas#Multiprogramación|Multiprogramación]], pues si existe un procesador disponible y además existen procesos en estado *ready*, el *scheduling* se encargará de la elección de uno de estos procesos para su ejecución.

## Schedulers
### Largo Plazo *(Job Scheduler)*
Selecciona un conjunto de procesos de una *jobs pool* y los carga en memoria para ser ejecutarlos, por lo tanto, controla el *grado de multiprogramación* (cantidad de procesos en memoria).

>[!important] Grado de Multiprogramación
>Si el *grado de multiprogramación* es estable, entonces el promedio de procesos entrando al sistema es equivalente al promedio de procesos saliendo del sistema.

### Medio Plazo *(Swapping)*
En ocasiones puede ser de utilidad remover procesos de la memoria y por lo tanto reducir el **grado de multiprogramación**. Luego estos procesos pueden ser reintroducidos en la memoria y su ejecución puede continuar donde se dejó.

### Corto Plazo *(CPU Scheduler)*
Selecciona un proceso de los que se encuentran en estado *ready* y le asigna el CPU para su ejecución.

Se invoca el **CPU Scheduler** en los siguientes casos:
1. Cuando un proceso pasa de estado *running* a *waiting*.
2. (Opcional) Cuando un proceso pasa de estado *running* a *ready*.
3. (Opcional) Cuando un proceso pasa de estado *waiting* a *ready*.
4. (Opcional) Cuando un proceso pasa de estado *new* a *ready*.
5. Cuando un proceso pasa al estado *terminated*.

>[!important] Expropiativo vs No-Expropiativo
>El scheduler es **expropiativo** cuando le quita el CPU al proceso que estaba haciendo uso del CPU *(casos 2, 3, 4)*. Por ende, el uso de un scheduler expropiativo o no dependerá del tipo de sistema que estemos implementando.

## Despachador
Se encarga de darle el control del CPU al proceso seleccionado por el *scheduling de corto plazo*.
Por lo tanto, se encarga de:
1. [[Procesos#Context Switch|Context Switch]].
2. Cambiar a modo usuario.
3. Saltar a la instrucción en la que se encuentra el proceso *(program counter)*.

>[!important] Dispatch Latency
>Se busca que el **despachador** sea lo más rápido posible, pues se invoca siempre que se intercambien procesos.
>
>El tiempo que toma detener un proceso y empezar otro se le conoce como *dispatch latency*.

## Clase de Procesos
Existen distintas políticas de scheduling dependiendo la clase de procesos que se ejecutan.
Los procesos tienen ciclos de ráfagas de ejecución *(CPU burst)* y ciclos de ráfagas de espera *(I/O burst)*.

- **Procesos CPU Bound**: Procesos que tienen alto uso del procesador.
- **Procesos I/O Bound**: Procesos que tienen alto uso de operaciones I/O.

## Criterios para comparar Algoritmos

## Afinidad de Procesador
En sistemas multiprocesadores simétricos *(SMP systems)* se intenta evitar la migración de un proceso desde un CPU a otro. A esto se le conoce como **afinidad de procesador**. Esto es conveniente para aprovechar la memoria cache del procesador y así aumentar el rendimiento del sistema.

>[!error] Desbalance
>Un problema que surge con la técnica de *afinidad de procesador*, es el desbalance en la cantidad de trabajo entre los procesadores.

## Algoritmos
Los diferentes algoritmos de scheduling pueden compararse según el siguiente criterio:
- **Utilización del CPU**: Se busca maximizar el porcentaje de uso del CPU.
- **Rendimiento**: Se busca maximizar la cantidad de procesos por unidad de tiempo.
- **Tiempo de Retorno**: Se utiliza un intervalo de tiempo desde que se cargó un proceso hasta que el mismo finaliza su ejecución.
- **Tiempo de Espera**: Es la suma de los periodos en la cola de espera.
- **Tiempo de Respuesta**: Es el intervalo de tiempo desde que un proceso es cargado hasta que da su primera respuesta. *(Útil en sistemas interactivos).*

### First Come First Server
Se ejecuta los procesos (hasta que finalicen) según el orden de arribo.

*Observación: sea $\{p_1,...,p_n\}$ un conjunto de procesos donde $p_i$ es el i-esimo proceso en arribar. Si se esta ejecutando $p_j$ y este recibe una petición de I/O, se empieza a ejecutar $p_{j+1}$ y cuando esta petición de I/O finalize, deja de ejecutarse $p_{j+1}$ y se sigue con la ejecución de $p_j$.*

### Shortest Job First
Se ejecuta el proceso que tenga la menor carga de trabaja hasta su finalización o hasta la próxima petición de I/O.

### Basados en Prioridad
A cada proceso se le asigna una prioridad, y el algoritmo se encarga de seleccionar el proceso con mas prioridad.

### Round Robin
Después de una cierta porción de tiempo *(time quantum)* se mueve el proceso que este en ejecución al final de una cola y se continua con el siguiente proceso.

### Multilevel Queue
Cada proceso es clasificado y asignado permanentemente a una cola donde cada una de estas utiliza su propio algoritmo. Además, se pueden implementer diferentes estrategias para definir si una cola tiene más prioridad que otra.

### Multilevel Feedback Queue
A diferencia de *Multilevel Queue* los procesos pueden cambiar de cola.
