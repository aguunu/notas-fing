Los circuitos lógicos combinatorios, o simplemente circuitos combinatorios, son circuitos elaborados a partir de compuertas o de otros circuitos del mismo tipo (usados como "bloque constructivo") cuya salida es una [[Álgebra de Boole#Función Lógica|Función Lógica]] de sus entradas y por tanto las salidas actuales sólo dependen del valor actual de las entradas.

## Bloques Constructivos
A continuación veremos algunos ejemplos de circuitos combinatorios útiles para ser utilizados como parte de diseños más complejos

### Circuito Decodificador
El *circuito decodificador* cuenta con $n$ entradas y $2^n$ salidas. La idea de este circuito combinatorio, es interpretar cada combinación de las $n$ entradas como el número que representan en binario, es decir, un número $i \in [0, 2^n - 1]$, de esta forma, la salida *i-esima* se activará únicamente cuando la combinación de entrada es la que representa el número asociado a la salida.

>[!example] 
>Para el caso de $n=2$, la [[Álgebra de Boole#Tabla de Verdad|Tabla de Verdad]] para el decodificador se representa de la siguiente forma:
>

|$A$|$B$|$Y_0$|$Y_1$|$Y_2$|$Y_3$|
|-|-|-|-|-|-|
|0|0|1|0|0|0|
|0|1|0|1|0|0|
|1|0|0|0|1|0|
|1|1|0|0|0|1|

>
>Siendo $A, B$ las entradas e $Y_i$ la salida *i-esima*.

### Circuito Multiplexor
El *circuito multiplexor* cuenta con $n$ entradas de control, $2^n$ entradas de datos, y $1$ salida. La idea de este circuito combinatorio es interpretar las $n$ entradas de control como el número $i \in [0, 2^n - 1]$ que representan en binario, luego, el valor de la salida coincide con la entrada de datos *i-esima*.

>[!example] 
>Para el caso de $n=2^2$, la [[Álgebra de Boole#Tabla de Verdad|Tabla de Verdad]] para el decodificador se representa de la siguiente forma:
>

|$A$|$B$|$Y$|
|-|-|-|
|0|0|$D_0$|
|0|1|$D_1$|
|1|0|$D_2$|
|1|1|$D_3$|

>
>Siendo $A, B$ las $n$ entradas de control, $D_i$ las $2^n$ entradas de datos, e $Y$ la salida.

### Circuito Demultiplexor
El *circuito demultiplexor* cuenta con $n$ entradas de control, $1$ entrada de datos, y $2^n$ salidas. Su comportamiento es similar al de un [[#Circuito Decodificador]]; interpreta cada combinación de las $n$ entradas como el número que representan en binario, es decir, un número $i \in [0, 2^n - 1]$, de esta forma, el valor de la salida *i-esima* será el mismo que la entrada de datos.

>[!example] 
>Para el caso de $n=2 + 1$, la [[Álgebra de Boole#Tabla de Verdad|Tabla de Verdad]] para el decodificador se representa de la siguiente forma:
>

|$A$|$B$|$D$|$Y_0$|$Y_1$|$Y_2$|$Y_3$|
|-|-|-|-|-|-|
|0|0|$D$|0|0|0|
|0|1|0|$D$|0|0|
|1|0|0|0|$D$|0|
|1|1|0|0|0|$D$|

>
>Siendo $A, B$ las entradas de control, $D$ la entrada de datos, e $Y_i$ la salida *i-esima*.

### Circuito Sumador Completo de 1-bit
Es un circuito que puede ser utilizado para construir sumadores de $n$ bits, mediante su conexión en "cascada". Para ello deberemos construir un sumador de dos números de $1$ bit cada uno con entrada y salida de acarreo (carry).

|$A$|$B$|$C_{in}$|$S$|$C_{out}$|
|-|-|-|-|-|
|0|0|0|0|0|
|0|0|1|1|0|
|0|1|0|1|0|
|0|1|1|0|1|
|1|0|0|1|0|
|1|0|1|0|1|
|1|1|0|0|1|
|1|1|1|1|1|
