La *Solución de Dekker* brinda una solución al [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] que consiste [[Sección Crítica#Busy Waiting|Busy Waiting]] y además es independiente del SO, es decir no utiliza [[Sistema Operativo#System Calls|System Calls]].

```c
/* Variables Globales */
desea_entrar : array of 2 booleans
turno : integer

/* Inicialización de las Variables Globales*/
desea_entrar[0] ← false
desea_entrar[1] ← false
turno ← 0 // o 1
```

```c
/* Estructura de P0 (análogo para P1) */
P0:
	desea_entrar[0] ← true
	while desea_entrar[1] {
		if turn ≠ 0 {
			desea_entrar[0] ← false
			while turno ≠ 0; // busy waiting
	        desea_entrar[0] ← true
	    }
	}
	
	// sección crítica
	...
	turno ← 1
	desea_entrar[0] ← false
	// sección restante
	...
```
