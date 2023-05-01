Existe un *buffer* con $n$ slots y cada slot es capaz de almacenar una unidad de datos. Además hay dos procesos ejecutándose llamados *consumidor* y *productor* que operan sobre el *buffer*.
El *productor* intenta insertar datos en el *buffer* mientras que el *consumidor* intenta remover datos del *buffer*, respetando las siguientes reglas:
- El *productor* no debe insertar datos cuando el buffer esta lleno.
- El *consumidor* no debe remover datos cuando el buffer esta vacío.
- El *productor* y *consumidor* no deben acceder al buffer simultáneamente.

## Solución con [[Semáforos]]
Se hace uso de los siguientes semáforos:
- Un semáforo binario `mutex` (inicialmente 1) usado para adquirir y liberar el buffer.
- Un semáforo de conteo `empty` que indica el número de slots vacíos en el buffer (inicialmente $n$).
- Un semáforo de conteo `full` que indica la cantidad de datos en el buffer (inicialmente 0).

```c
// Productor.
do {
	empty.P();
	mutex.P();
	// Insertar dato del buffer.
	// ...
	mutex.V();
	full.V();
} while (true);

// Consumidor.
do {
	full.P();
	mutex.P();
	// Remover dato del buffer.
	// ...
	mutex.V();
	empty.V();
} while (true);
```

