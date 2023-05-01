Un *monitor* es una abstracción que provee un mecanismo efectivo y conveniente para la sincronización de [[Procesos]] a través de [[Sincronización por Hardware]]. 

El *tipo monitor* define un conjunto de variables cuyos valores definen el estado de dicha instancia. Además, el monitor contiene un conjunto de operaciones que operan sobre dichas variables y a su vez proveen [[Sección Crítica#^8f593f|Exclusión Mutua]] dentro del monitor.

```c
Monitor nombre_monitor
{
	// Declaración de variables compartidas.
	// ...

	// Operaciones.
	function P1(...) { ... }
	function P2(...) { ... }
	// ...
	function Pn(...) { ... }

	// Codigo para inicializar el monitor.
	inicializar(...) { ... }
}
```

Una operación definida dentro de un monitor puede acceder únicamente a las variables declaradas localmente en el monitor y a los parámetros de dicha función. De forma similar, las variables locales pueden ser accedidas únicamente por estas operaciones.

Solo puede haber una única operación en ejecución en un momento dado.

Se definen variables de tipo *condition* cuyo valor no se inicializa. Las únicas operaciones que pueden ser invocadas sobre dichas variables son `wait()` y `signal()`.
Sea `var` una variable de tipo *condition*:
- `var.wait()`: El proceso que invoque esta función se bloquea y queda en un cola de procesos bloqueados.
- `var.signal()`: Si la cola de procesos no esta vacía, despierta al primer proceso bloqueado. En otro caso, la operación no tiene efecto.
