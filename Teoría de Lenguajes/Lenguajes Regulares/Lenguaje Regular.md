Decimos que un [[Lenguaje]] es *regular* si existe alguna instancia de los siguientes objetos matemáticos que lo generen:
- [[Expresiones Regulares]]
- [[Autómata Finito]]
	- [[Autómata Finito Determinista]]
	- [[Autómata Finito No-Determinista]]
	- [[Autómata Finito No-Determinista con Transiciones Epsilon]]
- [[Gramática Regular]]

## Relación $R_L$
Sea $L \subseteq \Sigma^\ast,\; x,y \in \Sigma^\ast$, definimos la relación $R_L$ como:

$$x R_{L} y \iff \forall z \in \Sigma^\ast \; (xz \in L \land yz \in L) \lor (xz \notin L \land yz \notin L)$$

## Relación $R_M$
Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ un [[Autómata Finito Determinista|AFD]], $x, y \in \Sigma^\ast$, definimos la relación $R_M$ como:

$$xR_My \iff \hat{\delta}(q_0, x) = \hat{\delta}(q_0, y)$$

***

> [!info]
> $R_M$ es una relación de equivalencia donde $|R_M|$ es igual a la cantidad de estados de $M$.
> 
> Además, para cualquier [[Expresiones Regulares|Lenguaje Regular]] $L$ se cumple que $xR_My \implies xR_Ly$. Por ende, se puede duducir que $|R_L| \leq |R_M|$.

>[!warning]
>No necesariamente se cumple que $xR_Ly \implies xR_My$.

## Propiedades de Clausura
Los [[#Lenguaje Regular|Lenguajes Regulares]] son cerrados bajo las siguientes operaciones:
1. **Unión**: Sean $L_1$ y $L_2$ regulares $\implies L_1 \cup L_2$ regular.
2. **Intersección**: Sean $L_1$ y $L_2$ regulares $\implies L_1 \cap L_2$ regular.
3. **Concatenación**: Sean $L_1$ y $L_2$ regulares $\implies L_1 \cdot L_2$  regular.
4. **Diferencia**: Sean $L_1$ y $L_2$ regulares $\implies$ $L_1 - L_2$ regular
5. **Clausura**: Sea $L$ regular $\implies L^\ast$ regular.
6. **Complementario**: Sea $L$ regular $\implies L^c$ regular.
7. **Reflexión**: Sea $L$ regular $\implies L^r$[^1] regular.
8. **Cociente**: Sea $L_1$ regular y $L_2$ un lenguaje arbitrario $\implies$ $\frac{L_1}{L_2}$[^2]  regular.
9. **Sustitución**: Sea $L$ regular y $f$ una función de sustitución $\implies f(L)$ regular.
10. **Homomorfismo**: Sea $L$ regular y $h$ un homomorfismo[^3] $\implies$ $h(L)$ regular.
11. **Homomorfismo Inverso**: Sea $L$ regular y $h$ un homomorfismo $\implies$ $h^{-1}(L)$ regular.

[^1]: Se define el reflexión/reverso de un lenguaje $L$ como $L^r=\{x^r \in \Sigma^\ast: x \in L\}$. 
[^2]: Se define el cociente entre los lenguajes $L_1$ y $L_2$ como $\frac{L_1}{L_2}=\{x \in \Sigma^\ast : \exists y \in L_2 \land xy \in L_1 \}$.
[^3]: Un homomorfismo de cadenas es una función sobre cadenas que sustituye cada símbolo por una cadena determinada. A modo de ejemplo, la función $h$ definida por $h(0) = ab$ y $h(1) = \varepsilon$ es un homomorfismo. Dada cualquier cadena formada por $0s$ y $1s$, todos los $0s$ se reemplazan por la cadena $ab$ y todos los $1s$ se reemplazan por $\varepsilon$. Por ejemplo $h(011)=h(0) \cdot h(1) \cdot h(1) = ab$.
