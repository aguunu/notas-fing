Una base de datos es utilizada entre varios procesos concurrentes. Algunos de estos desean únicamente leer datos mientras que otros desean modificar, es decir, leer y escribir datos.
Se distinguen los dos tipos de procesos como *lectores* y *escritores*.
Observar que si dos *lectores* desean acceder simultáneamente no habrán problemas. Sin embargo, si un *escritor* y cualquier otro proceso desea acceder podría conllevar a datos inconsistentes. Por lo tanto, se requiere que los *escritores* tengan acceso exclusivo a la base de datos.

## Solución con [[Semáforos]]
Se hace uso de los siguientes semáforos:
- Un semáforo binario `mutex` (inicializado en 1) usado para tomar control sobre `readcount` entre los *escritores*.
- Un semáforo binario `wrt` (inicializado en 1) usado para tomar control sobre la base de datos entre un *escritor* y los *lectores*.

Además contamos con un entero `readcount` que representa la cantidad de lectores sobre la base de datos.

```c
// Escritor.
do {
	wrt.P();
	// Realiza la modificación sobre la base de datos.
	// ...
	wrt.V();
} while (true);

// Lector.
do {
	mutex.P();
	readcount += 1;
	if (readcount == 1) {
		wrt.P();
	}
	mutex.V();
	// Realiza la lectura sobre la base de datos.
	// ...
	mutex.P();
	readcount -= 1;
	if (readcount == 0) {
		wrt.V();
	}
	mutex.V()
} while (true);
```

>[!info] Observación
>En esta solución estamos dando prioridad a los *lectores* sobre los *escritores* debido al uso del semáforo `wrt`.
