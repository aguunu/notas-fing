La técnica de *pipeline* apunta a mejorar el rendimiento del [[CPU]] sin aumentar la frecuencia de su reloj.

Un *pipeline* de $k$ etapas consiste en predecir las próximas $k$ instrucciones, de forma que cuando una instrucción finalice la etapa $i$ del [[CPU#Ciclo de Instrucción|Ciclo de Instrucción]], además de iniciar la próxima etapa $i+1$ en dicha instrucción (en caso de que exista una próxima etapa), también se empiece a ejecutar la etapa $i$ correspondiente a la siguiente instrucción predicha (en caso de que esta instrucción este dentro de las $k$ instrucciones predichas).

```mermaid
gantt
title Not Pipelined
axisformat %S%
	section Instrucción 1
		Fetch:F1, 0, 1s
		Decode:D1, after F1, 1s
		Read:R1, after D1, 1s
		Execute:E1, after R1, 1s
		Write:W1, after E1, 1s
	section Instrucción 2
		Fetch:F2, after W1, 1s
		Decode:D2, after F2, 1s
		Read:R2, after D2, 1s
		Execute:E2, after R2, 1s
		Write:W2, after E2, 1s
```

```mermaid
gantt
title Pipelined
axisformat %L%
	section Instrucción 1
		Fetch:F1, 0, 1s
		Decode:D1, after F1, 1s
		Read:R1, after D1, 1s
		Execute:E1, after R1, 1s
		Write:W1, after E1, 1s
	section Instrucción 2
		Fetch:F2, after F1, 1s
		Decode:D2, after F2 D1, 1s
		Read:R2, after D2 R1, 1s
		Execute:E2, after R2 E1, 1s
		Write:W2, after E2 W1, 1s
```

## Pipeline Hazards
Hay situaciones que generan problemas para el funcionamiento óptimo del *pipeline*.

### Hazards Estructurales
Surgen al existir conflicto de recursos de hardware entre distintas etapas del pipeline.

>[!example] 
>Supongamos que se ejecutan simultáneamente la etapa *read* y *fetch* de las instrucciones $i_1$, $i_2$ respectivamente. Por lo tanto, se produce un conflicto por el uso del [[Arquitectura de Computadores#Bus|Bus de Comunicación]]. Pues $i_1$ desea leer un operando en memoria, mientras que $i_2$ desea leer la instrucción 3 de memoria. Ambas acciones necesitan hacer uso de dicho bus.

*Una solución general es "burbuja de pipeline"[^burbuja-pipeline].*

### Hazards de Datos
Surgen al existir dependencias de datos entre instrucciones.

- Read After Write: Ocurre cuando una instrucción posterior lee un valor en memoria que será modificado por una instrucción anterior. Las posibles soluciones a este problema son:
	- *burbuja de pipeline*[^burbuja-pipeline].
	- *out of order execution*
	- *register forwarding*

>[!example] 
>  Si tenemos las siguientes instrucciones $i_1$, $i_2$:
>
> ```asm
> MOV [0xC8], 7
> ADD 0x1A, [0xC8]
> ```
>  Al hacer el *write* de $i_1$ después del *read* de $i_2$ el valor en `[0xC8]` no sería `7`, lo que generaría datos inconsistentes.

- Write After Read: Ocurre cuando una instrucción posterior escribe un registro que actúa como operando de una instrucción anterior antes que ésta pueda leerlo. *Este tipo de hazard no ocurre en los tipos de pipeline vistos.*
- Write After Write: Ocurre cuando una instrucción anterior escribe un registro que también actúa como resultado de una instrucción posterior después de ésta. *Este tipo de hazard no ocurre en los tipos de pipeline vistos.*

### Hazards de Control
Surgen al realizar modificaciones al registro `IP`.

Las técnicas para resolver los *hazards de control* incluyen:
- __Prefetch__: consiste en realizar simultáneamente el *fetch* de la próxima instrucción en memoria y de la instrucción apuntada por la dirección destino del salto. Cuando el salto se efectiviza la instrucción que no corresponde a la secuencia lógica se descarta.
- __Múltiples Flujos__: consiste en duplicar las etapas del pipeline que están ubicadas hasta la que decide el salto. De esta manera se puede avanzar en la ejecución de ambos flujos de instrucciones.
- __Salto Demorado__: siempre se ejecuta la instrucción que está luego del salto, en caso de que no exista dicha condición, se coloca un `NOP`.
- __Predicción de Salto__: consiste en determinar, en base a una política, si el salto se va a tomar o no. Existen las siguientes politicas:
	- Asumir que siempre o nunca se ejecuta el salto.
	- Predicción basada en la condición del salto: ciertos tipos de condición tienen mayor tendencia a realizar el salto y otros a no realizarlo.
	- Conmutar Taken / No Taken: predice el comportamiento de un salto en función de los antecedentes del salto anterior que no tiene por qué ser el mismo. Esto es bueno para bucles, pero no en general.
	- BHT (Branch History Table): se almacena en una tabla la información de un cierto conjunto de saltos recientemente evaluados.

## Out Of Order Execution
Se realiza la ejecución de instrucciones sin respetar el orden establecido por su ubicación en memoria (obviamente respetando el orden lógico).

>[!example] 
>Si tenemos las siguientes instrucciones:
>```asm
>MOV AX, [0x0FDE]
>MOV BX, 0xF0
>XOR CX, AX, 0x0F
>ADD AX, BX
>```
>No será necesario esperar por la ejecución de la instrucción `XOR` para ejecutar la instrucción `ADD`.

[^burbuja-pipeline]: La técnica de *burbuja de pipeline*, consiste esperar agregando artificialmente operaciones del tipo `NOP` *(No OPeration), que no requieren recursos.