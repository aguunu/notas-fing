La técnica de *segmentation* consiste en asignarle segmentos contiguos de memoria a un procesos para sus distintos sectores de memoria *(ej. stack, heap, código)*.
Cada segmento posee un *identificador* y *tamaño* asociado. De esta forma, una [[Virtual Memory#Virtual Address|Virtual Address]] de $m$ bits, se descompone de la siguiente manera:
- Los $m-n$ bits de mayor orden componen el *segment number*
- Los restantes $n$ bits, componen el *segment offset*.

>[!success] Protección
>Dividir la memoria en segmentos permite asociar a cada segmento *protection bits* que representarán un conjunto de permisos controlados a nivel de hardware.

## Segment Table
Estructura de datos que se almacena en memoria principal y se encarga de mapear una *virtual address* a una *physical address*. El registro *Segment Table Base Register (STBR)*  es accedido por el [[Memory Management Unity|MMU]] utiliza para tener una referencia a dicha estructura y así poder computar la *physical address* correspondiente.

El hardware provee registros *limit register/base register* que serán usados para computar la *physical address* asociada. En caso de no existir, se produce una [[Sistema Operativo#Excepción|Excepción]].

>[!success] Compartir Segmentos
>Si un proceso $p_0$ desea compartir un segmento con un proceso $p_1$, el sistema agregará dicho segmento en el [[#Segment Table]] asociado a $p_1$.


