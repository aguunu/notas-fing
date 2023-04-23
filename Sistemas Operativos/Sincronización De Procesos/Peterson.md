La *Solución de Peterson* resuelve el [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]]. Sin embargo, esta restringida a 2 [[Procesos]]. Además, se requiere compartir dos datos entre ellos.

```c
int turn; // indica el proceso al que le corresponde entrar a su sección crítica.
bool flag[2]; // indica si el proceso esta listo para entrar a su sección crítica.
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

>[!info]
>La *Solución de Peterson* se puede generalizar fácilmente para varios [[Procesos]].
