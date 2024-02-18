Una interrupción consiste en un mecanismo que le permite al hardware la invocación de una rutina fuera del control del programa que está siendo ejecutado.

Esto significa que cuando ocurre una interrupción la próxima instrucción a ser ejecutada no es la que esta siendo apuntada por el IP (Instruction Pointer), sino la primera instrucción de la *rutina de servicio de la interrupción* correspondiente al pedido atendido.

Por otra parte, no hay sincronismo entre la ejecución del programa y la, eventual, invocación a esa rutina "especial" disparada por la interrupción.

## Interrupt Request
Es mecanismo de interrupción comienza con el *interrupt request* generado por un [[Input & Output#Device Controller|Device Controller]]. Este dispositivo posee una entrada `INT` *(también conocida como `IRQ` o `INTR`)* asociada a un bit especifico de su *status register*, tomando el valor 1 cuando genera un *interrupt request*. Una vez se satisfaga el *interrupt request* el dispositivo actualiza dicho valor.
A su vez, la [[CPU]] posee una entrada `INT` para consultar sobre la existencia de algún *interrupt request*.

La [[CPU]] implementa el *interrupt request* de una de las siguientes formas:
- *Detección por Nivel:* Existe un *interrupt request* mientras la entrada `INT` del [[CPU]] se encuentre en nivel lógico 1.
- *Detección por Flanco:* Existe un *interrupt request* cuando la entrada `INT` del CPU cambia de 0 a 1.

Luego de realizar la etapa *write* del [[CPU#Ciclo de Instrucción|Ciclo de Instrucción]], la CPU consulta por *interrupt request*, en caso de que exista y se pueda *atender* la interrupción, suceden los siguientes eventos:
- Se salva el valor de `IP` ya sea utilizando el stack o registros especiales. *Notar: algunas arquitecturas suelen salvar más registros.*
- Se identifica mediante algún mecanismo el [[Input & Output#Device Controller|Device Controller]] que generó el *interrupt request*.
- Se obtiene la dirección de la rutina de atención correspondiente al [[Input & Output#Device Controller|Device Controller]] identificado. *Notar: por lo general las arquitecturas utilizan el mecanismo de vector de interrupciones.*
- Se *enmascaran* las interrupciones, es decir, impide la aceptación de *interrupt requests*.
- Se ejecuta la rutina de atención identificada, cargando en el registro `IP` la primer instrucción de la rutina.
- Se *desenmascaran* las interrupciones y se vuelve al estado anterior a la invocación de la interrupción.


>[!important] 
>[[8086]] utiliza un *vector de interrupciones* para obtener la dirección segmentada de la rutina de atención *CS:IP* (4 bytes). *Al atender una rutina de atención, se salvan los registros CS, IP, y FLAGS*.
>Además, para identificar la interrupción se utilizan 8 bits, por lo tanto, el vector podrá referenciar hasta $2^8$ rutinas.
>*Notar: [[8086]] presenta una instrucción `INT` que fuerza la ejecución de determinada rutina de atención.*
>
>Para *habilitar* las interrupciones en 8086 se utiliza la instrucción `STI` que se encarga de activar la *flag* `I`. Por otra parte, para *deshabilitar* las interrupciones se utiliza la instrucción `CLI`, desactivar dicha flag. *Notar: algunas CPU's poseen una entrada `NMI` (Non Maskable Interrupt) que ignoran la flag `I`.*
>Luego, para saber si existe un pedido efectivo de interrupción, se realiza el `AND` entre la flag `I`  y el pedido de interrupción por hardware.

### Identificación del Controlador

- Líneas `INT` independientes: el CPU se posee multiples entradas `INT`, cada dispositivo se conecta directamente a una de estas. Por lo tanto, el dispositivo que está pidiendo la interrupción es el que está conectado a la entrada `INT` donde se detecta la solicitud.
- Mecanismo `INT`/`INTA`: el CPU dispone de una única entrada de pedido de interrupción `INT`, a la cuál se conectan en modalidad OR-cableado todas las salidas `INT` de los dispositivos. También dispone de una salida denominada `INTA` *(Interrupt Acknowledge)* la cual se activa y se propaga mediante los dispositivos de forma encadenada, de esta forma, el primer dispositivo de la cadena que tenga un *interrupt request* pendiente colocará en el [[Arquitectura de Computadores#Bus|Bus de Datos]] su identificación para que el CPU obtenga dicha identificación.
![[Drawing 2024-02-17 17.23.32.excalidraw]]
*Observar: el mecanismo `INT`/`INTA` impone cierta prioridad al momento de elegir la interrupción a ser atendida.*
- Controlador de Interrupciones: es una variante al *mecanismo `INT`/`INTA`, donde se coloca un "controlador de interrupciones" que funciona como intermediaria entre las señales `INTA` e `INT`*
![[Drawing 2024-02-17 17.41.26.excalidraw]]