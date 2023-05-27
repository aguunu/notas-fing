Hay $n$ *filósofos* sentados en una mesa circular. Cada *filósofo* tiene delante un plato y cada plato un cubierto a su derecha. *Observar que en total hay $n$ platos y $n$ cubiertos sobre la mesa y cada plato tiene un cubierto a su derecha y otro a su izquierda.*
Si un *filósofo* desea comer, intentará tomar los dos cubiertos adyacentes a su respectivo plato, respetando las siguientes reglas:
- Un *filósofo* no podrá tomar cubiertos que estén siendo usados por otro *filósofo*.
- Cuando un *filósofo* este comiendo, liberará los cubiertos cuando este termine.

## Solución con [[Semáforos]]
Se hace uso de un arreglo `cubiertos[N] : Array of Mutex` de semáforos binarios (inicializados en 1) donde `N` equivale a la cantidad de cubiertos y  `cubiertos[i]` representa el cubierto en la posición $i$.

```c
// Filósofo i-esimo.
do {
	cubiertos[i].P();
	cubiertos[(i + 1) % N].P();
	// Comer
	// ...
	cubiertos[i].V();
	cubiertos[(i + 1) % N].V();
} while (true);
```

>[!bug] Deadlock
>En este código, si los $n$ filósofos desean comer simultáneamente, el programa quedaría en [[Deadlock]]. Una posible solución a este problema, seria permitirle a un filósofo tomar un cubierto si y solamente si ambos cubiertos están libres.

Para solucionar el problema, agregamos un arreglo `libre[N] : Array of Boolean` (inicializados en `false`) donde cada entrada equivale a un cubierto. Además agregamos un semáforo binario `m` (inicialmente 1) para adquirir y liberar el sistema.

```c
// Filósofo i-esimo.
do {
    m.P();
    if (libre[i] && libre[(i + 1) % N]) {
	    cubiertos[i].P();
	    libre[i] = false;
	    cubiertos[(i + 1) % N].P();
	    libre[(i + 1) % N] = false;
		m.V();
	    // Comer.
	    // ...
	    cubiertos[i].V();
	    libre[i] = true;
	    cubiertos[(i)];
	    libre[(i + 1) % N] = true;
    }
    else {
	    m.V()
	}
} while (true);
```

>[!success] Deadlock
>En esta última solución, si los $n$ filósofos desean comer simultáneamente, solo uno de ellos podrá adquirir el mutex `m`. Además, luego de adquirirlo, este tomará los cubiertos únicamente si ambos están libres, evitando de esta forma el problema de [[Deadlock]].

## Solución con [[Monitores]]
En esta solución un *filósofo* tomará ambos cubiertos únicamente si ambos están libres.

En esta solución, distinguimos el estado de cada *filósofo* usando `enum Estado = {PENSANDO, HAMBRIENTO, COMIENDO}`, y guardamos cada estado en `estados[N] : Array of Estado`.
Observar que el *filósofo i-esimo* puede cambiar su estado a `COMIENDO` solamente si sus dos vecinos no se encuentran `COMIENDO`.

```c
Monitor CenaFilosofos {
	estados[N]: Array of Estado;
	filósofos[N]: Array of Condition;

	void init() {
		for (int i = 0; i < N; i++) {
			estados[i] = PENSANDO;
		}
	}
	
	void tomar_cubiertos(int i) {
		estados[i] = HAMBRIENTO;
		check(i);
		if (estados[i] != COMIENDO) {
			filósofos[i].wait();
		}
	}

	void dejar_cubiertos(int i) {
		estados[i] = PENSANDO;
		check((i - 1) % N);
		check((i + 1) % N)
	}

	void check(int i) {
		if (estados[i] != HAMBRIENTO) {
			return;
		}
		
		if (estados[(i - 1) % N] != COMIENDO && estados[(i + 1) % N] != COMIENDO {
			estados[i] = COMIENDO;
			filósofos[i].signal();
		}
	}
}
```
