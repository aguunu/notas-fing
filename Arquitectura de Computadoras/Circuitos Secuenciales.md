Los *circuitos secuenciales*, a diferencia de los [[Circuitos Lógicos Combinatorios|Combinatorios]] determinan el valor de sus salidas no solo en función del valor actual de sus entradas sino que también en función de los valores anteriores de las mismas.

Un *circuito secuencial* se define a través de sus ecuaciones:

$$Y = G(X, E) \tag{Función de Salida}$$

$$E' = H(X, E) \tag{Función de Transición}$$

Siendo $Y$ la salida, $X$ la entrada, $E$ el estado interno e $E'$ el nuevo estado luego de la transición.

## Diseño de Circuitos Secuenciales
El diseño de un circuito secuencial en base a las máquinas de estado se realiza en base a la especificación del [[Autómata Con Salida]] que define el comportamiento esperado del circuito. Los estados se almacenan en *flip-flops* (tipo [[Flip-Flops#Flip-Flop J-K|JK]] ó [[Flip-Flops#Flip-Flop D|D]], sincrónicos por flanco) y las funciones de salida y transición se implementan en lógica combinatoria.

En base a estos principios de diseño, se pueden establecer las siguientes etapas, las que deben ser ejecutadas para obtener el diseño del circuito:
1. [Opcional] Modelado del sistema a implementar mediante la especificación del [[Autómata Con Salida]] correspondiente mediante un diagrama.
2. Deducir la **Tabla de Estados**.
3. Determinar cantidad de bits y sistema de codificación para la(s) entrada(s) y la(s) salida(s).
4. Determinar el número de [[Flip-Flops]] necesarios para codificar todos los estados posibles del sistema y determinar la codificación a utilizar.
5. Incorporar la codificación de los estados, entradas y salidas a la **Tabla de Estados** para obtener la **Tabla de Transiciones y Salidas**.
6. Seleccionar los [[Flip-Flops]] a utilizar y en base a las ecuaciones de los mismos pasar de la **Tabla de Transiciones y Salidas** a las [[Álgebra de Boole#Tabla de Verdad|Tablas de Verdad]] de las [[Álgebra de Boole#Función Lógica|Funciones Lógicas]] que permitirán determinar el valor de la(s) salida(s) en base a la(s) entrada(s) y las salidas de los [[Flip-Flops]], y el valor a presentar en las entradas de los [[Flip-Flops]] para almacenar el nuevo estado en ellos.
7. Minimizar las expresiones lógicas en dos niveles mediante un método sistemático *(ej. [[Álgebra de Boole#Diagrama de Karnaugh|Karnaugh]])*.
8. Dibujar el circuito lógico resultante en base a los [[Flip-Flops]] y compuertas básicas (AND, OR y NOT).
