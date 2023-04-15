Un lenguaje es un conjunto (posiblemente infinito) de cadenas, todas ellas seleccionadas de un $\Sigma^\star$, donde $\Sigma$ es un determinado [[Conceptos Fundamentales#Alfabetos|Alfabeto]].

1. El lenguaje de todas las cadenas que constan de $n$ ceros seguidos de $n$ unos para cualquier $n \ge 0$: $\{\varepsilon,01,0011,000111,...\}$.
2. $\Sigma^\star$ es un lenguaje para cualquier alfabeto $\Sigma$.
3. $\emptyset$, el lenguaje vacío, es un lenguaje de cualquier alfabeto.
4. $\{\varepsilon \}$, el lenguaje que consta sólo de la cadena vacía, también es un lenguaje de cualquier alfabeto. *Observe que $\emptyset \neq \{\varepsilon\}$; el primero no contiene ninguna cadena y el segundo sólo tiene una cadena.*

Aunque los lenguajes pueden tener un número infinito de cadenas, están restringidos a que dichas cadenas estén formadas por los símbolos que definen un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] prefijado.

## Lenguaje Regular
Un leguaje $L$ es regular si existe una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $r$ define a $L$.

Se cumplen las siguientes propiedades:
1. Sean $L_1$ y $L_2$ lenguajes regulares $\implies L_1 \cup L_2$ es un lenguaje regular.
2. Sean $L_1$ y $L_2$ lenguajes regulares $\implies L_1 \cdot L_2$ es un lenguaje regular.
3. Sea $L$ un lenguaje regular $\implies L^\star$ es un lenguaje regular.
4. Sea $L$ un lenguaje regular $\implies L^c$ es un lenguaje regular.
5. Sean $L_1$ y $L_2$ lenguajes regulares $\implies L_1 \cap L_2$ es un lenguaje regular.
6. Sea $L$ un lenguaje regular $\implies L^r$ *(el reverso de $L$)*[^1] es un lenguaje regular.
7. Sea $L_1$ un lenguaje regular y $L_2$ un lenguaje arbitrario $\implies$ $\frac{L_1}{L_2}$ *(cociente de lenguajes)*[^2]  es un lenguaje regular.
8. Sea $L$ un lenguaje regular y $f$ una función de sustitución $\implies f(L)$ es un lenguaje regular.
9. Sea $L$ un lenguaje regular y $h$ un homomorfismo $\implies$ $h(L)$ es un lenguaje regular.
10. Sea $L$ un lenguaje regular y $h$ un homomorfismo $\implies$ $h^{-1}(L)$ es un lenguaje regular.

## Relaciones
Sea $L \subseteq \Sigma^\star,\; x,y \in \Sigma^\star$  entonces, $$x R_{L} y \iff \forall z \in \Sigma^\star \; (xz \in L \land yz \in L) \lor (xz \notin L \land yz \notin L)$$
Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ un [[Autómata Finito Determinista|AFD]] entonces, $$xR_My \iff \hat{\delta}(q_0, x) = \hat{\delta}(q_0, y)$$
*Observación: $|R_M|$ es equivalente a la cantidad de estados de $M$.*

*Observación: no necesariamente se cumple que $xR_Ly \implies xR_My$. Sin embargo, si se cumple que $xR_My \implies xR_Ly$. Por ende,  $|R_L| \leq |R_M|$.*

[^1]: Sea $L$ un lenguaje, se define el reverso $L^r=\{x^r \in \Sigma^\star: x \in L\}$. 
[^2]: Sea $L_1$ y $L_2$ lenguajes, se define el cociente $\frac{L_1}{L_2}=\{x \in \Sigma^\star : \exists y \in L_2 \land xy \in L_1 \}$.
