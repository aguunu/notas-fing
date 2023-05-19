La *Solución de Dekker* brinda una solución al [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] que consiste [[Sección Crítica#Busy Waiting|Busy Waiting]].

```c
int turn; // Indica el proceso al que le corresponde entrar a su sección crítica.
bool flag[2]; // Indica si el proceso esta listo para entrar a su sección crítica.
```

Sean $P_0$ y $P_1$ dichos procesos, la estructura del proceso $P_0$ según la solución de Peterson:

```c
flag[0] = true; 
turn = 1;
while (flag[1] && turn == 1); // busy waiting
// Sección crítica.
// ...
flag[0] = false;
// Sección restante.
// ...
```

Análogamente, se deduce la estructura del proceso $P_1$.

>[!info] Observación
>A pesar que la *Solución de Peterson* esta restringida a 2 procesos, esta se puede generalizar fácilmente para varios [[Procesos]].
