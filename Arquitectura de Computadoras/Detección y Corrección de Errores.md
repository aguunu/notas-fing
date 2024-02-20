Todo **sistemas de codificación** que permita detección y corrección de errores se basa en la *redundancia*. Pues, para saber si una representación binaria es valida, se debe agregar información adicional a dicha representación. Por lo tanto, todo sistema de codificación que permita detección de errores, cumple que la cantidad de **representaciones validas** es menor a la cantidad de **representaciones**.

## Distancia
La distancia entre dos representaciones binarias se define como la cantidad de bits distintos entre las dos representaciones. En otras palabras, la distancia entre dos representaciones esta dada por la cantidad de $1's$  en el $XOR$ entre ambas representaciones.

>[!example] 
>Sean $a=01101, b=10110$ representaciones binarias, entonces:
>
>$$d(a, b) = |a \oplus b|_1 = |01101 \oplus 10110|_1 = |11011|_1 = 4$$

$$\tag{1} d(a,b) = d(b, a)$$

$$\tag{2} d(a,b) = 0 \iff a = b$$

$$\tag{3} d(a, b) + d(b, c) \geq d(a, c)$$

Se define *distancia de sistema de codificación* como la mínima distancia que existe entre dos representaciones validas distintas de dicho sistema.

## Detección y Corrección
Consideramos un *sistema de codificación* con distancia $d$, dos representaciones binarias $a$ y $b$ *validas*. Definimos el conjunto $A = \{a' \mid d(a, a') \leq e\}$, es decir, el conjunto de representaciones obtenidas al modificar $e$ bits de $a$. Análogamente definimos $B$.

![[Drawing 2024-02-08 17.34.29.excalidraw]]

Observar que para poder *detectar* errores, se debe cumplir la siguiente ecuación.
$$a \notin B \land b \notin A \iff d(a, b) > e \iff \textcolor{red}{d > e}$$
Por otro lado, para poder *corregir* errores además de detectarlos, se debe cumplir la siguiente ecuación.
$$A \nsubseteq B \land B \nsubseteq A \iff A \cap B = \emptyset \iff d(a, b) > 2e \iff \textcolor{red}{d > 2e}$$

## Bits de Redundancia
Para generar un *sistema de codificación* de $k$ bits que pueda *detectar* y *corregir* errores de hasta 1 bit *Observar que el sistema deberá ser de distancia mayor o igual a 3, pues $e=1$.*

En primer lugar, deberemos agregar $p$ bits de *redundancia* para poder identificar el bit erróneo y además un bit extra indicar que no hay error. Por ende, la representación tendrá $k + p + 1$ bits y deberá cumplir la siguiente ecuación.
$$2^p \geq k + p + 1$$

## Paridad de 1 bit
Permite la detección de errores de 1 bit agregando un bit de paridad en la representación para que la cantidad de $1's$ en la nueva representación sea par *(paridad par)* o impar *(paridad impar)*. El bit de paridad se calcula de la siguiente forma.
$$
p=\begin{cases}
\overline{b_ 0 \oplus b_1 \oplus \cdots \oplus b_n}, & \textit{si paridad impar} \\
b_ 0 \oplus b_1 \oplus \cdots \oplus b_n, & \textit{si paridad par} \\
\end{cases}
$$

Luego, para chequear si existe error, basta con realizar el mismo procedimiento y corroborar la paridad.

## 2 de 5
#TODO

## Códigos de Hamming
Los *Códigos de Hamming* se utilizan para detectar y corregir errores de 1 bit en representaciones de distancia $3$.

Sean $a_1a_2a_3a_4$ los bits de información, necesitamos satisfacer $2^p \geq 4 + p + 1$, por ende, necesitamos $3$ bits de redundancia ($p_1p_2p_3$).

Luego, generamos la representación como $a_4 a_3 a_2 p_3 a_1 p_2 p_1$, calculando los bits de redundancia de la siguiente forma:
- $p_1 = a_4 \oplus a_2 \oplus a_1$
- $p_2 = a_4 \oplus a_3 \oplus a_1$
- $p_3 = a_4 \oplus a_3 \oplus a_2$

Luego, al recibir una representación, hallamos la paridad de la siguiente manera:
- $s_1 = p_1 \oplus a_4 \oplus a_2 \oplus a_1$
- $s_2 = p_2 \oplus a_4 \oplus a_3 \oplus a_1$
- $s_3 = p_3 \oplus a_4 \oplus a_3 \oplus a_2$

|  | $a_4$ | $a_3$ | $a_2$ | $p_3$ | $a_1$ | $p_2$ | $p_1$ |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| $s_1$ | x |  | x |  | x |  | x |
| $s_2$ | x | x |  |  | x | x |  |
| $s_3$ | x | x | x | x |  |  |  |

Donde $s=s_3 s_2 s_1$ representa un entero en binario. Si $s=0$ no hay errores. Por otra parte, si $s \neq 0$ índica que hay un bit invalido en la representación y la posición de este bit (leído de derecha a izquierda) es indicada por $s$.

## Checksum
Consiste en agregarle a una representación binaria un código adicional que se calcula como la suma de los códigos transmitidos módulo $2^n$, siendo $n$ la cantidad de bits del código.

>[!example] 
>Se envía el siguiente código $0110 \; 1001 \; 1101$. Entonces, calculamos el *checksum* como $(0110 + 1001 + 1101) \mod{2^4} = (0001 \; 1100) \mod{2^4} = 1100$.
>
>Luego, el mensaje completo sería $0110 \; 1001 \; 1101 \; \color{red}1100$

## Cyclic Redundancy Check
En primer lugar, ambas partes acuerdan un patrón $G$ de $r + 1$ bits. Luego, el objetivo de *cyclic redundancy check (CRC)* al transmitir un mensaje $D$, es encontrar un código $R$ de $r$ bits que cumpla $DR \pmod{G} = 0$. Por lo tanto, el receptor detectará un error si $DR \pmod{G} \neq 0$.

>[!tip] 
>Necesitamos hallar $R$ que cumpla $D \cdot 2^r \oplus R \pmod G = 0$.
>*Notar: $D \cdot 2^r$ equivale a $D$ al aplicarle un desplazamiento de $r$ bits hacia izquierda. Mientras que $\oplus$ equivale a la suma bit a bit.*
>
>Por ende, podremos calcular $R$ con la siguiente formula:
>$$R=D \cdot 2^r \pmod G$$
