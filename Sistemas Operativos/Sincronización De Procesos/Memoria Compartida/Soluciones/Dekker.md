La *Solución de Dekker* brinda una solución al [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] que consiste [[Sección Crítica#Busy Waiting|Busy Waiting]].

```c
int turn; // Indica el proceso al que le corresponde entrar a su sección crítica.
bool flag[2]; // Indica si el proceso esta listo para entrar a su sección crítica.
```

Sean $P_0$ y $P_1$ dichos procesos, la estructura del proceso $P_i$ según la solución de Dekker:

```c
flag[0] ← true
while (flag[1]) {
	if (turn != 0) {
		flag[0] = false
		while (turno != 0) {}; // busy waiting
	    flag[0] = true
	}
}
// Sección crítica.
// ...
turn = 1
flag[0] = false
// Sección restante.
// ...
```

Análogamente, se deduce la estructura del proceso $P_1$.
