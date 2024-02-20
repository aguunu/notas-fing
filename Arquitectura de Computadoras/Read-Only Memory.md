Una *read-only memory (ROM)* es un [[Circuitos Combinatorios|Circuito Combinatorio]] que cuenta con $m + 2$ entradas $A_0, A_1, \dots, A_{m-1}, CS, OE$, y $n$ salidas $D_0, D-1, \dots, D_{n-1}$. Además, la [[Álgebra de Boole#Tabla de Verdad|Tabla de Verdad]] de una ROM esta formada por $2^m$ filas y $n$ columnas.

>[!success] 
>Una ROM podrá implementar cualquier función lógica de $m$ variables y $n$ salidas.

## Capacidad y Organización
Las memorias ROM están caracterizadas por una cierta capacidad, que se mide en bits y una determinada organización, que se expresa en cantidad de palabras de tantos bits.

>[!example]
>- ROM de 8 kbit, con organización de 1Kx8 (1 Kilo palabras de 8 bits)
>- ROM de 8 kbit, con organización de 4Kx2 (4 Kilo palabras de 2 bits)
>- ROM de 1 kbit, con organización de 1Kx1 (1 Kilo palabras de 1 bit)

## Arreglos de Memoria
Las memorias se utilizan en combinaciones denominados __*bancos de memoria*__. Estos bancos permiten la construcción de memorias del tamaño requerido por el sistema en base a circuitos integrados disponibles.

## Chip Select
La entrada CS (Chip Select) permite ahorrar en la implementación la estructura de ANDs que estamos colocando a la salida de las ROMs para elegir cual de ellas conecta a la salida en función del bit más significativo de la dirección.
1. $\texttt{CS = 0} \rightarrow$ Todas las salidas de la ROM están en 0.
2. $\texttt{CS = 1} \rightarrow$ Todas las salidas presentan el contenido de la ROM en la posición señalada por la dirección.

## Lógica de Tercer Estado
Es un circuito que presenta 3 salidas diferentes: $0,1,Z$. El estado $Z$ es conocido como __*tri-state*__.

Los circuitos que poseen este tipo de salida también poseen una entrada denominada *OE (Output Enable)*.
1. $\texttt{OE = 0} \rightarrow$ La salida pasa a *tri-state*.
2. $\texttt{OE = 1} \rightarrow$ La salida pasa al valor lógico 0 o 1.

Por ende, haciendo uso del *tri-state* se puede implementar __*or-cableado*__[^1], pues al haber un tercer estado, no se producirá un cortocircuito.[^2]

>[!warning] 
>El *tri-state* no se propaga por las compuertas. Es una condición que solo aplica a la salida.

[^1]: En lugar de usar una compuerta $OR$ con las entradas $a,b$ y salida $Y$, se conectan directamente los cables $a$ y $b$ a la salida $Y$.
[^2]: Se produce cuando una salida $Y$ recibe dos valores distintos $0$ y $1$ lo que dañando el circuito, específicamente las salidas $a$ y $b$ que se fueron unidas.
