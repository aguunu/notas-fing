Todo **sistemas de codificación** que permita detección y corrección de errores se basa en la *redundancia*. Pues, para saber si una representación binaria es valida, se debe agregar información adicional a dicha representación. Por lo tanto, todo sistema de codificación que permita detección de errores, cumple que la cantidad de **representaciones validas** es menor a la cantidad de **representaciones**.

## Distancia
La distancia entre dos representaciones binarias se define como la cantidad de bits distintos entre las dos representaciones. En otras palabras, la distancia entre dos representaciones esta dada por la cantidad de $1's$  en el $XOR$ entre ambas representaciones.

>[!example] 
>Sean $a=01101, b=10110$ representaciones binarias, entonces:
>
>$$d(a, b) = a \oplus b = 01101 \oplus 10110 = 4$$

$$\tag{1} d(a,b) = d(b, a)$$

$$\tag{2} d(a,b) = 0 \iff a = b$$

$$\tag{3} d(a, b) + d(b, c) \geq d(a, c)$$

En sistemas de codificación, se define *distancia de sistema de codificación* a la mínima distancia que existe entre dos representaciones validas de dicho sistema.

## Detección y Corrección de Errores
Si consideramos un *sistema de codificación* con distancia $d$ y dos representaciones binarias $a$ y $b$ **validas** dentro del sistema. Sea $A$ el conjunto de representaciones (no necesariamente validas) obtenidas al modificar $e$ bits de $a$. Análogamente definimos $B$.
Si se cumple que $A \cap B = \emptyset$, además de poder detectar errores, también podremos reconocer a que **representación valida** corresponde una **representación invalida**.
Por otro lado, podemos detectar errores, siempre y cuando $a \notin B \land b \notin A$, pues en caso de no cumplirse estas condiciones, $a$ podría ser una representación invalida de $b$, lo cual no podríamos detectar como error.

>[!tldr]
>Para que el *sistema de codificación* pueda detectar errores, es necesario que se cumpla la siguiente condición:

$$a \notin B \land b \notin A \iff d < e$$

Por otra parte, para que el *sistema de codificación* además de detectar, pueda corregir errores, es necesaria que se cumpla la siguiente condición:

$$A \cap B = \emptyset \iff d < \frac{e}{2}$$

## Bits de Redundancia
Para generar un *sistema de codificación* de $k$ bits con distancia $3$, se necesitan $p$ bits para "señalar" cuál es el bit invalido. Además de $1$ bit para indicar si hay o no error en la representación. Por lo tanto, se deberá cumplir la siguiente condición:

$$2^p \geq k + p + 1$$

Donde $2^p$ es la cantidad de posiciones que se pueden "señalar", observar que esta cantidad deberá ser mayor o igual a la cantidad de bits de la representación, en este caso, $k$ bits de información, $p+1$ bits de redundancia, donde el último de estos índica si hay o no error.

## Paridad de 1 bit
Se agrega un bit de paridad a cada representación para que la cantidad de $1's$ en la representación (incluyendo el bit de paridad) sea par (paridad par) o impar (paridad impar).

>[!error] 
>Esta técnica se basa en que la probabilidad de que falle un bit es extremadamente baja. Por lo tanto, puede tener un mal comportamiento cuando hay más de $1$ bit invalido. $(\star)$

Observar que dada una representación $b_0b_1...b_n$, podemos expresar su bit de paridad como $P = b_ 0 \oplus b_1 \oplus ... \oplus b_n$ (paridad par) y $P = \overline{b_ 0 \oplus b_1 \oplus ... \oplus b_n}$ (paridad impar). Luego, una vez obtenido $P$, podremos chequear si se detectaron errores $E = P \oplus b_0 \oplus b_1 ... \oplus b_n$. Si $E=0$, entonces no se detectaron errores $(\star)$.

## 2 de 5
#TODO

## Códigos de Hamming
Los *Códigos de Hamming* se utilizan para generar representaciones con distancia $3$.

Sean $a_1a_2a_3a_4$ los bits de información, por visto anteriormente, necesitamos $3$ bits de redundancia $p_1p_2p_3$ (pues $2^3 \geq 4 + 3 + 1$).

Luego, generamos la representación como $a_4 a_3 a_2 p_3 a_1 p_2 p_1$, calculando los bits de redundancia de la siguiente forma:
- $p_1 = a_4 \oplus a_2 \oplus a_1$
- $p_2 = a_4 \oplus a_3 \oplus a_1$
- $p_3 = a_4 \oplus a_3 \oplus a_2$

Luego, al recibir una representación, hallamos la paridad de la siguiente manera:

| |$a_4$|$a_3$|$a_2$|$p_3$|$a_1$|$p_2$|$p_1$|
|-|-|-|-|-|-|-|-|
|$S_1$|x||x||x||x|
|$S_2$|x|x||x|x||
|$S_3$|x|x|x|x|||

- $S_1 = p_1 \oplus a_4 \oplus a_2 \oplus a_1$
- $S_2 = p_2 \oplus a_4 \oplus a_3 \oplus a_1$
- $S_3 = p_3 \oplus a_4 \oplus a_3 \oplus a_2$

Donde $S=S_3 S_2 S_1$ representa un entero en binario. Si $S=0$ no hay errores. Por otra parte, si $S \neq 0$ índica que hay un bit invalido en la representación y la posición de este bit (leído de derecha a izquierda) es indicada por $S$.

## Checksum
Consiste en agregarle a un conjunto de códigos binarios transmitidos un código adicional que se calcula como la suma de los códigos transmitidos módulo $2^n$, siendo $n$ la cantidad de bits del código.

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
