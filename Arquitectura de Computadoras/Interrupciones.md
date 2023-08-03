Una interrupción consiste en un mecanismo que le permite al hardware la invocación de una rutina fuera del control del programa que está siendo ejecutado.

Esto significa que cuando ocurre una interrupción la próxima instrucción a ser ejecutada no es la que esta siendo apuntada por el IP (Instruction Pointer), sino la primera instrucción de la *rutina de servicio de la interrupción* correspondiente al pedido atendido.

Por otra parte, no hay sincronismo entre la ejecución del programa y la, eventual, invocación a esa rutina "especial" disparada por la interrupción.