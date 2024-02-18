
## Representación Binaria
Sea $n \in \mathbb{Z^+}$, entonces su representación binaria coincide con su expresión en base 2.
- Rango $k$ bits: $0 \leq n \leq 2^k - 1$.
- Operaciones: $\{ +, -, \cdot, \div \}$

>[!example] 
>Observar que $9 = \textcolor{green}{1} \cdot 2^3 + \textcolor{green}{0} \cdot 2^2 + \textcolor{green}{0} \cdot 2^1 + \textcolor{green}{1} \cdot 2^0$ siendo $\textcolor{green}{1001}$ su representación.

## Valor Absoluto & Signo
Sea $n \in \mathbb{Z}$, entonces se representa el $|n|$ con su [[#Representación Binaria]]. Luego el bit más significativo indicará el signo del entero; $1$ en caso de ser negativo, $0$ en caso de ser positivo.
- Rango $k$ bits: $-(2^k - 1) \leq n \leq 2^k - 1$.
- Operaciones: $\emptyset$
- Observaciones:
	1. Existen dos representaciones distintas para el $0$ que surgen al invertir su signo.

## Complemento a 1
El complemento a uno de $n \in \mathbb{Z}$, expresado en el *sistema binario* con largo $k$, se define como:

$$
C_1(n) \rightarrow
\begin{cases}
n,  & \text{si $n \geq 0$} \\
\overline{n}, & \text{si $n \leq 0$}
\end{cases}
$$

- Rango $k$ bits: $-(2^k - 1) \leq n \leq 2^k - 1$.
- Operaciones: $\emptyset$
- Observaciones:
	1. Existen dos representaciones distintas para $0$.
	2. $C_1(C_1(n))=n$

>[!example] 
>Con $k=4$ bits, la representación de $5=0101$ mientras que la representación de $-5=1010$.

## Desplazamiento
Se utiliza un desplazamiento $d$ fijo, luego, la representación de un entero $n$ será la [[#Representación Binaria]] de $n + d$.

$$D(n) \rightarrow n+D$$

- Rango $k$ bits: $0 \leq n \leq 2^k + d$
-  Operaciones: $\emptyset$
- Observaciones:
	1. Se conserva el orden de los números.
	2. Existe una única representación para el $0$.

## Complemento a 2
El complemento a dos de $n \in \mathbb{Z}$, expresado en el *sistema binario* con largo $k$, se define como:

$$
C_2(n) \rightarrow
\begin{cases}
n,  & \text{si $n \geq 0$} \\
\overline{n}+1, & \text{si $n < 0$}
\end{cases}
$$

Otra forma de definirlo es la siguiente:

$$C_2(n) \rightarrow 2^k - n$$

>[!tip] 
>En complemento a dos de $n$ bits, la representación $b_{n-1}b_{n} \dots b_0$ representa el número $\textcolor{yellow}{-b_{n-1}} 2^{n-1} + b_{n-2} 2^{n-2} + \dots + b_0 2^0$ en decimal. *==Notar el signo negativo respecto al bit más significativo de la representación.==*

- Rango $k$ bits: $-2^{k-1} \leq n \leq 2^{k-1} - 1$
- Observaciones:
	1. El $0$ tiene una única representación ($0 = \overline{0} + 1$).
	2. Operaciones: $\{+, -, \cdot, \div\}$
	3. $A-B=A+(-B)=A+(\overline{B}+1)$
	4. No se mantiene el orden.
	5. El bit de *carry* no indica por si solo *overflow*.
	6. $C_2(C_2(n))=n$

>[!danger] 
>En *complemento a 2*, el *overflow* ocurre al sumar dos números de igual signo obteniendo el signo opuesto en el resultado. Además, podemos calcular la flag de la siguiente forma:
>$$\texttt{Overflow} = \texttt{Carry\_Out} \oplus \texttt{Carry\_On}$$

## Binary-Coded Decimal
En la representación *binary-coded decimal (BCD)*, se codifican números decimales. Donde cada digito es representado por $4$ bits. Los 4 bits menos significativos marcan el signo y el final del número. Siendo $1100_2$ el fin de un número positivo y $1101_2$ el fin de un número negativo.

|Símbolo|4 bits|
|-|-|
|0|0000|
|1|0001|
|2|0010|
|3|0011|
|4|0100|
|5|0101|
|6|0110|
|7|0111|
|8|1000|
|9|1001|
|+|1100|
|-|1101|

>[!example] 
>$BCD(1234_{10})=0001 \; 0010 \; 0011 \; 0100 \; 1100$

## Punto Flotante
Los números reales con representación en punto flotante normalizado, en base $\beta$, están dados por la siguiente expresión:

$$PF(x)=(-1)^s \cdot 1,\overset{\textit{mantisa: $m$}}{\overbrace{m_1 m_2 \dots m_p}} \cdot \beta^{e-p} = (-1)^s \cdot m \cdot \beta^{e-d}$$

donde:
- $0 \leq m_i \leq \beta - 1$.
- $L \leq e \leq U$.
- $s \rightarrow$ parámetro del signo. Puede valer $1 \; (-)$ o $0 \; (+)$.
- $m \rightarrow$ mantisa.
- $(e - p) \rightarrow$ exponente.

La normalización viene en el hecho de que $\beta^{-1} \leq m < 1$; evitando que los números tengan distintas representaciones posibles.

### IEEE 754
Se utiliza $\beta=2$ y la mantisa normalizada es de la forma $1,m_1 m_2 \cdots m_p$. Mientras que la mantisa des-normalizada es de la forma $0,m_1 m_2 ... m_p$.

$$\tag{Normalizado} PF(x) = (-1)^s \cdot \textcolor{red}{1},m \cdot 2^{e-d}$$

$$\tag{Desnormalizado} PF(x)=(-1)^S \cdot \textcolor{red}{0},m \cdot 2^{e-d}$$

$m$ tendrá $p$ bits asignados, $e$ tendrá $q$ bits asignados, y s $s$ tendrá 1 bit asignado, por lo que la suma de los bits asignados serán $N=1+q+p$.

|Bits Asignados|$s$ *(signo)*|$q$ *(exponente)*|$p$ *(mantisa)*|
|---|---|---|---|
|$(\star)$ Precisión Media *(16-bits)*|1|5|10|
|Precisión Simple *(32-bits)*|1|8|23|
|Precisión Doble *(64-bits)*|1|11|52|

Para la representación de exponentes negativos, es necesario un desplazamiento viable $(d)$, y así obtener un rango viable de exponentes.

$$E = e-(2^{q-1} - 1) = e-d \implies d = 2^{q-1} - 1$$

| |$E=(e-p)$ *(exponente)*|$m$ *(mantisa)*|
|---|---|---|
|Normalizados|$0 \dots 0 < E < 1 \dots 1$|Cualquiera|
|Desnormalizado|$0 \dots 0$|$\neq 0$|
|Cero|$0 \dots 0$|$0$|
|Infinito|$1 \dots 1$|$0$|
|NaN|$1 \dots 1$|$\neq 0$|

Luego, la representación del código binario de $PF(x)$ se vería como la concatenación de las representaciones binarias de $s \cdot e \cdot m$. Observar que el desplazamiento $(d)$ y la base $(\beta)$ están fijas y dependen de la representación.
