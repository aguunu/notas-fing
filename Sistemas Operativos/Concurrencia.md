## Sección Crítica
La sección crítica es una sección de código donde múltiples procesos intentan acceder a un recurso compartido o realizar una tarea crítica al mismo tiempo.

Cuando varios procesos intentan acceder simultáneamente a un recurso compartido, pueden ocurrir problemas como *race conditions*, en los que el resultado final del programa depende del orden en que los procesos acceden al recurso compartido. Este problema se denomina "*El Problema de la Sección Crítica*".

Para resolver este problema, se busca diseñar un protocolo que los procesos utilicen para cooperar entre ellos, y que a su vez cumplan con las siguientes condiciones:
1. **Exclusión Mutua**: Si un proceso esta ejecutando su sección crítica, ningún otro proceso podrá estar ejecutando en dicha sección crítica. ^7b522d
2. **Progreso**: Si varios procesos desean entrar a una sección crítica y esta se libera, la misma deberá ser asignada a uno de estos procesos. (Evita [[#Deadlock]]).
3. **Espera Acotada**: Existe un limite en la cantidad de veces que un proceso es permitido entrar en su sección crítica después de que otro proceso realizó una petición para entrar a su sección crítica. (Evita espera indefinida).

*Observación: el problema de sección crítica se puede generalizar para ser aplicado tanto a [[Procesos]] como a [[Threads]].*

### Busy Waiting
Desperdicia ciclos del CPU que podrían ser aprovechados por otro proceso.
```c
// busy waiting
while (condicion); // no hacer nada
```

### Deadlock
Dos o más procesos están esperando indefinidamente por un evento que puede ser causado únicamente por alguno de estos procesos.

## Entrelazado
TODO

## Solución de Dekker
La solución de Dekker, es independiente del SO (no utiliza [[Estructura del SO#System Calls|System Calls]]) pues utiliza [[#Busy Waiting]].

*Observación: esta solución no se utiliza en la práctica.*

## Solución de Peterson
Esta solución esta restringida a 2 procesos. Se requiere compartir dos datos entre dichos procesos:
```c
int turn; // indica el proceso al que le corresponde entrar a su sección crítica.
boolean flag[2]; // indica si el proceso esta listo para entrar a su sección crítica.
```

Sean $P_i$ y $P_j$ dichos procesos, la estructura del proceso $P_i$ según la solución de Peterson:
```c
do {
	flag[i] = true; 
	turn = j;
	while (flag[j] && turn == j); // busy waiting
	/* sección crítica */
	flag[i] = false;
	/* sección restante */
} while(true);
```
Análogamente, se deduce la estructura del proceso $P_j$

*Observación: la solución de Peterson se puede generalizar fácilmente para varios procesos.*

## Sincronización por Hardware
Las soluciones eficientes para el problema de sección crítica requieren asistencia del hardware y del SO.
Todas estas soluciones se basan en *locking*, encargándose de proteger las secciones críticas a través de *locks*.

### Test And Set && Compare And Swap
El problema de sección crítica puede ser resuelto fácilmente en un sistema *single-processor* si pudiéramos deshabilitar las [[Interrupciones]] mientras la variable compartida esta siendo modificada. Sin embargo, en un sistema *multi-processor* consumiría mucho tiempo (el mensaje se pasaría a todos los procesadores).
A pesar de esto, los sistemas modernos proveen instrucciones de hardware atómicas para resolver este problema. `test_and_set()` y `compare_and_swap()`.

Existe una variable compartida entre los procesos que puede tomar el valor 0 o 1. Antes de entrar a una sección crítica adquieren un *lock*, que luego liberarán al salir. Si este está *lock* esta bloqueado, el proceso espera hasta que se desbloque. En otro caso, toma el *lock* y ejecuta la sección crítica.

```c
/* Operacion atómica test_and_set */
boolean test_and_set(boolean *target) {
	boolean rv = *target;
	*target = true;
	return rv;
}

/* Operacion atómica compare_and_swap */
int compare_and_swap(int *value, int expected, int new_value) {
	int temp = *value;
	if (*value == expected)
		*value = new value;
	return temp;
}
```

*Exclusion Mutua* con *test and set*:
```c
do {
	while (test_and_set(&lock)); // busy waiting
	/* sección crítica */
	lock = false;
	/* sección restante */
} while (true);
```

*Exclusion Mutua* con *compare and swap*:
```c
do {
	while (compare and swap(&lock, 0, 1) != 0); // busy waiting
	/* sección crítica */
	lock = 0;
	/* sección restante */
} while (true);
```

*Observación: tanto la solución con `test_and_set()` y `compare_and_swap()` hacen uso de [[#Busy Waiting]]*.

### Semáforos
Es una técnica para administrar procesos concurrentes haciendo uso de un único *valor entero no negativo* compartido entre estos procesos, este valor se se conoce como *semáforo* que resuelve el [[#Problema de Sección Crítica]] y logra la sincronización entre procesos en [[Sistemas Operativos/Introducción#Sistema Multiprocesador (Paralelos)|Multiprocessing Systems]].

Un semáforo es un valor entero no negativo, que se accede únicamente por dos operaciones atómicas:
- `wait()` $\rightarrow$ **P** *to test*
- `signal()` $\rightarrow$ **V** *to increment*

```c
/* Operación atómica P "to test" */
void wait(Semaforo S) {
	while (S <= 0); // busy waiting
	S--;
}

/* Operación atómica V "to increment" */
void signal(Semaforo S) {
	S++;
}

/* Inicializa el semáforo S */
void init(unsigned int S, unsigned int recursos_disponibles) {
	S = recursos_disponibles;
}
```

```c
wait(S); // esperar hasta que el semáforo S este disponible
/* sección crítica */
signal(S); // avisar a los procesos que el semáforo S esta disponible
/* sección restante */
```

#### Semáforo Binario
El semáforo binario puede tomar el valor 0 o 1. En algunos sistemas, también se le conocen como **Mutex Locks** ya que son *locks* que proveen [[#^7b522d|Exclusión Mutua]].

#### Semáforo de Conteo
El semáforo de conteo no está restringido por un dominio. Se utiliza para controlar el acceso a un recurso que posee multiples instancias.

*Observación: se puede demostrar que los [[#Semáforo Binario]] y [[#Semáforo de Conteo]] son equivalentes.*

### Monitores
Un *monitor* es una abstracción que provee un mecanismo efectivo y conveniente para la sincronización de procesos. 

El *tipo monitor* define un conjunto de variables cuyos valores definen el estado de dicha instancia. Además, el monitor contiene un conjunto de operaciones que operan sobre dichas variables y a su vez proveen [[#^7b522d|Exclusión Mutua]] dentro del monitor.

```c
Monitor nombre_monitor
{
	/* declaración de variables compartidas */

	/* operaciones */
	function P1(...) { ... }
	function P2(...) { ... }
	.
	.
	.
	function Pn(...) { ... }

	/* codigo para inicializar el monitor*/
	inicializar(...) { ... }
}
```

Una operación definida dentro de un monitor puede acceder únicamente a las variables declaradas localmente en el monitor y a los parámetros de dicha función. De forma similar, las variables locales pueden ser accedidas únicamente por estas operaciones.

Solo puede haber una única operación en ejecución en un momento dado.

Se definen variables de tipo *condition* cuyo valor no se inicializa. Las únicas operaciones que pueden ser invocadas sobre dichas variables son `wait()` y `signal()`.
- `var_c.wait()`: El proceso invocando esta operación sera suspendido hasta que otro proceso invoque `var.signal()`.
- `var_c.signal()`: Se reanuda exactamente un proceso que se encuentre suspendido.

*Observación: en el caso de invocar `signal()` sin procesos bloqueados, la operación no tiene efecto.*