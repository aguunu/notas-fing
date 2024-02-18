El *álgebra de Boole* es una estructura matemática, que cuenta con dos números ($0$ y $1$) y tres operaciones (suma, producto y negación).

## Axiomas

$$\tag{Axioma 1} A+0=A$$

$$\tag{Axioma 2} A \cdot 1=A$$

$$\tag{Axioma 3} A+B=B+A$$

$$\tag{Axioma 4} A \cdot B= B \cdot A$$

$$\tag{Axioma 5} (A + B) + C = A + (B + C)$$

$$\tag{Axioma 6} (A \cdot B) \cdot C = A \cdot (B \cdot C)$$

$$\tag{Axioma 7} A \cdot (B + C) = (A \cdot B) + (A \cdot C)$$

$$\tag{Axioma 8} A + (B \cdot C) = (A + B) \cdot (A + C)$$

$$\tag{Axioma 9} \textit{para todo $A$ existe un $\bar{A}$ tal que } A \cdot \bar{A} = 0 \textit{ y } A + \bar{A} = 1$$

$$\tag{Axioma 10} \textit{cerrado bajo las operaciones de suma, producto y negación}$$

## Teoremas

$$\tag{Teorema 1} A + A = A$$

$$\tag{Teorema 2} A \cdot A = A$$

$$\tag{Teorema 3}A \cdot 0 = 0$$

$$\tag{Teorema 4}A + 1 = 1$$

$$\tag{Teorema 5}A + A \cdot B = A$$

$$\tag{Teorema 6}A + \bar{A} \cdot B = A + B$$

$$\tag{Teorema 7}A \cdot (A + B) = A$$

$$\tag{Teorema 8}A \cdot (\bar{A} + B) = A \cdot B$$

$$\tag{Teorema 9}\bar{A} \cdot (A + \bar{B}) = \bar{A} \cdot \bar{B}$$

$$\tag{Teorema 10}(\bar{A} + \bar{B}) \cdot (\bar{A} + \bar{B}) = \bar{A}$$

## Leyes de De Morgan

$$\tag{DM 1}\overline{A + B} = \bar{A} \cdot \bar{B}$$

$$\tag{DM 2}\overline{A \cdot B} = \bar{A} + \bar{B}$$

***
## Variable Lógica
Una **variable lógica** $A$ es aquella que puede tomar únicamente dos valores: $0$ y $1$.

## Función Lógica
Una **función lógica** $f$ es un conjunto de [[#Variable Lógica|Variables Lógicas]] $A, B, C$, relacionadas por los símbolos de las operaciones permitidas: suma, producto y negación.

Una función lógica acepta sólo dos posibles entradas ($0$ y $1$) y produce un solo valor (salida).

Alternativamente, se puede definir una función lógica $f$ según en que posiciones de la salida vale $0$ o $1$ usando $\prod$ y $\Sigma$ respectivamente.

>[!example]
> La función $f$ tal que $f(A, B, C)$ cumple que $f(A, B, C) = \Sigma(1, 4, 5, 6, 7) = \prod(0, 2, 3)$.

## Tabla de Verdad
Una **tabla de verdad** es una tabla donde se recoge el valor de la función para las diferentes combinaciones posibles de las variables. Si hay $n$ variables, tendremos $2^n$ combinaciones posibles.

## XOR
El *XOR $(\oplus)$* se define como $a \oplus b = \bar{a} \cdot b + a \cdot \bar{b}$ y cumple con ciertas propiedades.
1. Es la suma aritmética binaria módulo $2$.
2. Asociativa.
3. Conmutativa.
4. Distributiva: $a \cdot (b \oplus c) = (a \cdot b) \oplus (a \cdot c)$.
5. $a \oplus 0 = a$.
6. $a \oplus 1 = \bar{a}$.
7. $a \oplus a = 0$.
8. Cancelativa: $a \oplus b = a \oplus c \implies b = c$.

## Operadores Lógicamente Completos
Un conjunto de operadores se llama lógicamente completo si cualquier función booleana puede expresarse mediante los mismos.

## Karnaugh
Es un método de simplificación, donde se representa la función en un *Karnaugh-map* y luego se simplifica agrupando $1's$ en grupos de potencia de 2.
![[Drawing 2024-02-09 19.38.34.excalidraw]]

En este caso, la función se simplifica a $f(a, b, c, d) = \textcolor{skyblue}{a b c} + \textcolor{red}{c \hat{d}} + \textcolor{green}{b \hat{d}}$.

