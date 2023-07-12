Los *Flip-Flop* son [[Circuitos Secuenciales]] y se los pueden ver como un circuitos capaces de "recordar" el valor de la entrada previo al actual.

## Entradas Adicionales
En la práctica, los *flip-flops* cuentan con las siguientes entradas adicionales:
- Utilizadas en *flip-flops* sincrónicos y se activa por flanco:
	- Set: Pone en 1 el valor del circuito.
	- Clear: Pone en 0 el valor del circuito.
- Clock Enable: Fija el estado del *clock*.

## Flip-Flop R-S
El *Flip-Flop R-S* también conocido como *latch*, cuenta con 2 entradas $R$ y $S$, y 2 salidas $Q$ y $\bar{Q}$.
Su tabla de verdad corresponde con la siguiente:

|$R$|$S$|$Q_{n+1}$|
|-|-|-|
|0|0|$Q_n$|
|0|1|1|
|1|0|0|
|1|1|-|

- Asincrónico: Las funciones que generan los valores de las señales $R$ y $S$ pueden variar en cualquier momento.
- Sincrónico: Se introduce una señal de sincronismo para el circuito *(entrada de clock $CLK$)*, de esta forma, se actualizará los nuevos valores cuando se produzca un *tick*.

>[!error] 
>Cuando $M=S=1$, el estado $Q_{n+1}$ quedará indefinido.

## Flip-Flop D
Es una variante del [[#Flip-Flop R-S]], donde su tabla de verdad es la siguiente:

|$D$|$Q_{n+1}$|
|-|-|
|0|0|
|1|1|

Por ende, podemos escribir la función de la siguiente forma:

$$Q_{n+1} = D_n$$

## Flip-Flop T
Es un *flip-flop* mantiene su salida incambiada en el tiempo o la invierte en cada flanco.

|$T$|$Q_{n+1}$|
|-|-|
|0|$Q_n$|
|1|$\overline{Q_n}$|

Por ende, podemos escribir la función de la siguiente forma:

$$Q_{n+1} = \overline{T} \cdot Q_n + T \cdot \overline{Q_n}$$

## Flip-Flop J-K
Es construido a partir de dos [[#Flip-Flop R-S]] asincrónicos, donde su tabla de verdad es la siguiente:

|$J$|$K$|$Q_n$|$Q_{n+1}$|
|-|-|-|-|
|0|0|0|0|
|0|0|1|1|
|0|1|0|0|
|0|1|1|0|
|1|0|0|1|
|1|0|1|1|
|1|1|0|1|
|1|1|1|0|

Minimizando la función $Q_{n+1}$, obtenemos la siguiente función:

$$Q_{n+1}=J \cdot \overline{Q_n} + \overline{K} \cdot Q_n$$

Por ende, podemos re-escribir la tabla de verdad de la siguiente forma:

|$J$|$K$$|$Q_{n+1}$|
|-|-|-|
|0|0|$Q_n$|
|0|1|0|
|1|0|1|
|1|1|$\overline{Q_n}$

>[!success] 
>El *flip-flop J-K* se caracteriza por eliminar el estado indefinido que surge en el [[#Flip-Flop R-S]] cuando $J=K=1$.
