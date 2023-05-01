El hardware provee las instrucciones atómicas `test_and_set()` y `swap()` para resolver el [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]].

Existe una variable compartida entre los [[Procesos]] que puede tomar el valor 0 o 1. Antes de entrar a una [[Sección Crítica]], se adquiere un *lock*, que luego se liberará al salir. Si el *lock* adquirido esta bloqueado , el proceso espera hasta que se desbloque. En otro caso, toma el *lock* y ejecuta la sección crítica.

```c
// Operacion atómica test_and_set.
boolean test_and_set(boolean* target) {
	boolean rv = *target;
	*target = true;
	return rv;
}

// Operacion atómica swap.
int swap(int& a, int& b) {
	int tmp = a;
	a = b;
	b = tmp;
}
```

Solución al [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] con *test and set*:

```c
do {
	while (test_and_set(&lock)); // busy waiting
	// Sección crítica.
	// ...
	lock = false;
	// Sección restante.
	// ...
} while (true);
```

Solución al [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] con *swap*:

```c
bool lock = false; // Variable global, se inicializa una única vez.

do {
	bool key = true;
	while (key) { // busy waiting
		swap(&key, &lock);
	}
	// Sección crítica.
	// ...
	lock = false;
	// Sección restante.
	// ...
} while (true);
```

>[!warning] ¡Cuidado!
>A pesar de que ambas soluciones garantizan *exclusión mutua* y *progreso*, no garantizan *espera acotada*. Además utilizan *busy waiting*.
