El lenguaje de programación ADA, provee soporte para [[Concurrencia]] en el lenguaje.

>[!tip] TASK
>Una `TASK` representa un thread de ejecución independiente. A su vez, es inicializada automáticamente al comienzo de la ejecución del programa. Por ende, un programa termina su ejecución cuando finalizan todas sus `TASK`.
>
>Una `TASK` se compone de dos partes, una especificación y un cuerpo.

```
PROCEDURE [NOMBRE_PROCEDIMIENTO] IS
	-- Especificación del TASK
	TASK [NOMBRE_TASK] IS
	BEGIN
		ENTRY [NOMBRE_ENTRY](...);
		...
		ENTRY [NOMBRE_ENTRY](...);
	END TASK

	-- Cuerpo del TASK
	TASK BODY [NOMBRE_TASK] IS
	VAR [VARIABLE] : [TIPO];
	...
	VAR [VARIABLE] : [TIPO];
	BEGIN
		...
	END BODY
END PROCEDURE
```

Donde un `ENTRY` puede ser invocado por cualquier `TASK` que tenga acceso a dicho `ENTRY`, a este evento se le denomina *entry call*. 

```
[NOMBRE_TASK].[NOMBRE_ENTRY]([PARM], [PARM], ...);
```

Para que se realize una *entry call*, la `TASK` que define la `ENTRY` que se invoca, deberá incorporar en la lógica de su código la sentencia `ACCEPT` correspondiente a dicho `ENTRY`.

```
ACCEPT NOMBRE_ENTRY(PARM_I, PARM_II, ...) DO
	-- Código dentro de la sentencia ACCEPT
END ACCEPT
-- Código fuera de la sentencia ACCEPT
```

El `TASK` que invoque un `ENTRY`, deberá esperar/bloquearse hasta que se acepte y finalize la *entry call*, es decir, esperar a que se acepte y ejecute la sentencia `ACCEPT` correspondiente a dicho `ENTRY`.

Por otro lado, el `TASK` que define el `ENTRY`, permanecerá bloqueado en la sentencia `ACCEPT` hasta que se invoque el `ENTRY` correspondiente.

Esta sincronización se denomina *rendezvous*.

***

La sentencia `SELECT`, espera simultáneamente por *entry calls* en más de un `ACCEPT` y responde al que llegue primero usando la sentencia `OR`. En caso de no haber un *entry call* esperando por atención, se ejecuta inmediatamente el código de la sentencia `ELSE`.

```
SELECT
	ACCEPT [NOMBRE_ENTRY](...) DO
		...
	END ACCEPT
	...
	OR ACCEPT [NOMBRE_ENTRY](...) DO
		...
	END ACCEPT
	...
	ELSE
		...
END SELECT
```

La clausula/guarda `WHEN`, nos permite activar/desactivar las sentencias `ACCEPT` dentro de un `SELECT`.

Por otro lado, se provee una sentencia `DELAY` que espera cierta cantidad a recibir una *entry call* en alguna de las clausulas activas. En caso de que esto suceda, se acepta dicho `ENTRY`, en otro caso, se ejecutará el código de la sentencia `DELAY`.

```
SELECT
	WHEN (condición) => ACCEPT [NOMBRE_ENTRY](...) DO
		-- Código
	END ACCEPT
	-- Código
	OR ACCEPT [NOMBRE_ENTRY](...) DO
		-- Código
	END ACCEPT
	-- Código
	OR DELAY [SEGUNDOS]
		-- Código
	 ELSE
		-- Código
END SELECT
```

>[!warning] 
>La clausula `WHEN` es evaluada antes de entrar a la sentencia `SELECT`.

>[!error] 
>Si ninguna clausula es evaluada en `TRUE`, el programa abortará.

***
El atributo `COUNT` de una `ENTRY` indica la cantidad de *entry calls* están esperando por su atención. Sin embargo, este atributo solo aplica para el `TASK` que define dicho `ENTRY`.

```
IF ([NOMBRE_ENTRY]'COUNT > 0)
	...
```

***
En la especificación de un `TASK` podemos optar por usar `TASK TYPE` en vez de `TASK`, esto nos permite declarar un tipo de tarea para luego generar instancias sobre este tipo.

```
-- Especificación del TASK TYPE
TASK TYPE [NOMBRE_TASK_TYPE] IS
BEGIN
	ENTRY [NOMBRE_ENTRY](...);
	...
	ENTRY [NOMBRE_ENTRY](...);
END TASK

-- Cuerpo del TASK_TYPE
TASK BODY [NOMBRE_TASK_TYPE] IS
VAR [VARIABLE] : [TIPO];
VAR [VARIABLE] : [TIPO];
...
BEGIN
	-- CODIGO
END BODY
```

Podemos crear un conjunto de instancias de un determinado `TASK TYPE` en alguna estructura de datos *(ej. un arreglo)*.

```
THREADS := ARRAY(4) OF [NOMBRE_TASK_TYPE];
```
