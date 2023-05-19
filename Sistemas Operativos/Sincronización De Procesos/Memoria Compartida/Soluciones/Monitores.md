Un *monitor* es una abstracción que provee un mecanismo efectivo y conveniente para la sincronización de [[Procesos]] a través de [[Sincronización por Hardware]]. 

El *tipo monitor* define un conjunto de variables cuyos valores definen el estado de dicha instancia. Además, el monitor contiene un conjunto de operaciones que operan sobre dichas variables y a su vez proveen [[Sección Crítica#^8f593f|Exclusión Mutua]] dentro del monitor.

```c
Monitor [NOMBRE_MONITOR]
{
	// Declaración de variables compartidas.
	// ...

	// Codigo para inicializar el monitor.
	inicializar(...) { ... }
	
	// Operaciones.
	fn [OPERACION_0](...) { ... }
	fn [OPERACION_1](...) { ... }
	// ...
	fn [OPERACION_N](...) { ... }
}
```

Una operación definida dentro de un monitor puede acceder únicamente a las variables locales del monitor y a los parámetros de dicha función. De forma similar, las variables locales pueden ser accedidas únicamente por estas operaciones.

Solo puede haber una única operación en ejecución en un momento dado.

Se definen variables de tipo *condition* cuyo valor no es inicializado. Las únicas operaciones que pueden ser invocadas sobre dichas variables son `wait()` y `signal()`.
Sea `var` una variable de tipo *condition*:
- `var.wait()`: El proceso que invoque esta función se bloquea y queda en un *queue* de procesos bloqueados.
- `var.signal()`: Despierta al primer proceso bloqueado. Si la *queue* esta vacía, no tiene efecto.

## Bloqueo de Variables de Condición
Cuando un procedimiento invoca la operación `signal()`, el proceso que invoca `signal()` y el proceso que se despierta pueden siguen activos dentro del monitor.

Sea $p_0$ el proceso que invoca la operación `signal()` y $p_1$ el proceso que despierta, entonces,
- **Semántica de Hoare y Hansen**: $p_0$ devuelve el monitor y espera en una *queue*. $p_1$ inicia su trabajo inmediatamente.
- **Semántica de Mesa**: $p_0$ inserta a $p_1$ en una *ready queue* y sigue trabajando. Cuando $p_0$ finaliza, empieza a trabajar el primer proceso de dicha *queue*.

Si se ubican las operaciones `signal()` como última instrucción en el código, permite igualar ambas semánticas. *Observar que el proceso que invoque `signal()` dejará el monitor.*

### Estados de los Procesos
La semántica del monitor queda definida por las prioridades entre las diferentes *queues*.

- **Entry Queue**: Procesos que desean entrar al monitor *(prioridad E)*.
- **Waiting Queue**: Procesos que ejecutaron `wait()` y recibieron un `signal()` *(Prioridad W)*.
- **Signaler Queue**: Procesos que ejecutaron `signal()` *(prioridad S)*.
***
## Monitores $\equiv$ Semáforos
Podemos demostrar que los [[Monitores]] son equivalentes a los [[Semáforos]], pues ambos se pueden implementar entre ellos.

### Monitores $\rightarrow$ Semáforos

```c
Monitor Semáforo {
	cont: Integer;
	bloq: Condition;

	void init() {
		cont = N;
	}
	
	void P() {
		if (cont == 0) {
			bloque.wait();
		}
		cont -= 1;
	}

	void V() {
		cont += 1;
		bloque.signal();
	}
}
```

### Semáforos $\rightarrow$ Monitores

```c
/*
	cond : Integer;
	mutex : Semáforo Binario;
	condM : Semáforo;
*/

cond = 0;
mutex.INIT(1);
condM.INIT(0);

void WAIT() {
	cond += 1;
	mutex.V();
	condM.P();
	mutex.P();
}

void SIGNAL() {
	if (cond > 0) {
		cond -= 1;
		condM.V();
	}
}

void OPERACION_I {
	mutex.P();
	// Código Operación I.
	// ...
	mutex.V();
}
```
