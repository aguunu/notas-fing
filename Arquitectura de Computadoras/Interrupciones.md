***
Una interrupción consiste en un mecanismo que le permite al hardware la invocación de una rutina fuera del control del programa que está siendo ejecutado.

Esto significa que cuando ocurre una interrupción la próxima instrucción a ser ejecutada no es la que esta siendo apuntada por el IP (Instruction Pointer), sino la primera instrucción de la *rutina de servicio de la interrupción* correspondiente al pedido atendido.

Por otra parte, no hay sincronismo entre la ejecución del programa y la, eventual, invocación a esa rutina "especial" disparada por la interrupción.
***
Una interrupción es un mecanismo que permite al hardware la invocación de una rutina fuera del control del programa que está siendo ejecutado.

## Pedido de Interrupción
El mecanismo de interrupción comienza con el pedido de interrupción generado por un controlador de E/S.

### Detectar Interrupción
- Detección por Nivel: La CPU reconocerá que hay un pedido de interrupción pendiente mientras su entrada *INT* este en el nivel 1.
- Detección por Flanco: La CPU reconocerá que hay un pedido de interrupción cuando existe un flanco (un cambio de nivel 0 a nivel 1).

### Atención del Pedido de Interrupción
Cuando la CPU reconoce que hay un pedido de interrupción, comienza el mecanismo de atención a dicha solicitud que consta de los siguientes pasos:
1. Termina de ejecutar la instrucción actual.
2. Salva el valor actual del *Instruction Pointer (IP)*.
3. Identifica el controlador de E/S que realizó la interrupción.
4. Obtiene la dirección de la rutina de la interrupción correspondiente al controlador identificado.
5. Enmascara las interrupciones.
6. Ejecuta la rutina de interrupción.

#### Identificar Controlador
##### Líneas INT/IRQ independientes en la CPU  (Hardware)
En este caso la CPU tiene varias líneas INT numeradas, entonces la idea es conectar cada controlador E/S a cada una de ellas.

##### Mecanismo INT/INTA  (Hardware)
La CPU dispone de una única entrada de pedido de interrupción INT, a la cual se le conecta por un *OR Cableado* todos los pedidos de interrupción de los distintos controladores de E/S. También dispone de la salida *Interrupt Acknowledge (INTA)* que le "avisa" al controlador de E/S que se ha aceptado su solicitud de interrupción y por ende que coloque en el bus de datos su identificación, luego la CPU realiza una lectura sobre el bus de datos y obtiene el identificador.

##### Controlador de Interrupciones  (Hardware)
TODO

##### Identificación por Software (Software)
TODO

## Habilitación de Interrupciones
La CPU tiene la capacidad de aceptar o no los pedidos de interrupción de los controladores de E/S, esta capacidad esta implementada de dos maneras:
- Enmascaramiento (General)
- Deshabilitación (Selectiva)

## Prioridades
- Hay dos (o más) pedidos de interrupción simultáneos.
- Hay uno (o más) pedidos de interrupción mientras se esta ejecutando una rutina de interrupción previa y las interrupciones han sido habilitadas.
