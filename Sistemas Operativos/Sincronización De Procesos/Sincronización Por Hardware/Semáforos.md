El *semáforo* logra resolver el [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] y en [[Sistemas#Sistema Multiprocesador (Paralelos)|Multiprocessing Systems]]. Haciendo uso de un valor entero no negativo, que se accede únicamente por dos operaciones atómicas:
- `wait()` $\rightarrow$ **P** *to test*
- `signal()` $\rightarrow$ **V** *to increment*

```c
// Operación atómica P "to test".
void wait(Semaforo S) {
	while (S <= 0); // busy waiting
	S--;
}

// Operación atómica V "to increment".
void signal(Semaforo S) {
	S++;
}

// Inicializa el semáforo S.
void init(unsigned int S, unsigned int recursos_disponibles) {
	S = recursos_disponibles;
}
```

```c
wait(S); // Esperar hasta que el semáforo S este disponible.
// Sección crítica.
// ...
signal(S); // Avisar a los procesos que el semáforo S esta disponible.
// Sección restante.
// ...
```

## Semáforo Binario
El *semáforo binario (mutex)* puede tomar únicamente el valor 0 o 1. En algunos sistemas, también se le conocen como **Mutex Locks** ya que son *locks* que proveen [[Sección Crítica#^8f593f|Exclusión Mutua]].

>[!info] Observación
>Usar la operación `V()` sobre un *semáforo binario* cuyo valor es 1, la operación no tendrá efecto.

## Semáforo de Conteo
El *semáforo de conteo* no está restringido por un dominio. Se utiliza para controlar el acceso a un recurso que posee multiples instancias.

***
## Equivalencia
Se puede demostrar que los [[#Semáforo Binario]] y [[#Semáforo de Conteo]] son equivalentes ya que se puede implementar uno de estos a partir del otro.

## Semáforo de Conteo $\rightarrow$ Semáforo Binario
Se hace uso de las siguientes variables:
- `access`: Un semáforo de conteo para controlar el acceso a los demás datos (actúa como semáforo binario pues su valor será 0 o 1).
- `lock`: Un semáforo de conteo para bloquear threads cuando no hay recursos disponibles.
- `waiting_threads`: Threads que están esperando por la liberación del recurso.
- `worker_available`: Cantidad de recursos disponibles (0 o 1)

```c
void INIT_CONTEO(bool worker_available) {
	access.INIT(1)
	lock.INIT(0)
	waiting_threads = 0;
	worker_available = worker_available;
}

void V_BINARIO() {
	access.p();
	if (waiting_threads) > 0 {
		waiting_threads -= 1;
		lock.V();
	}
	else {
		worker_available = true;
	}
	access.V();
}

void P_BINARIO() {
	access.P();
	if (worker_available) {
		worker_available = false;
		access.V();
	} else {
		waiting_threads += 1;
		access.V();
		lock.P();
	}
}
```

## Semáforo Binario $\rightarrow$ Semáforo de Conteo
Se hace uso de las siguientes variables:
- `access`: Un semáforo binario para controlar el acceso a los demás datos.
- `threads_waiting`: Un semáforo binario utilizado por los threads para "avisar" de que están esperando a que se libere algún recurso.
- `available_workers`: Cantidad de recursos disponibles.

```c
void INIT_CONTEO(int workers) {
	access.INIT(1);
	threads_waiting.INIT(0);
	available_workers = workers;
}

void V_CONTEO() {
	access.P();
	available_workers += 1;
	if (available_workers < 0) {
		threads_waiting.V();
	}
	access.V();
}

void P_CONTEO() {
	access.P();
	available_workers -= 1;
	if (available_workers < 0) {
		access.V();		
		threads_waiting.P();
	} else {
		access.V();
	}
}
```
