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

## Semáforo de Conteo
El *semáforo de conteo* no está restringido por un dominio. Se utiliza para controlar el acceso a un recurso que posee multiples instancias.

> [!important] Equivalencia
> Se puede demostrar que los [[#Semáforo Binario]] y [[#Semáforo de Conteo]] son equivalentes ya que se puede implementar uno de estos a partir del otro.
