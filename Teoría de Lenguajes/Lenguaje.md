Un lenguaje es un conjunto (posiblemente infinito) de cadenas, todas ellas seleccionadas de un $\Sigma^*$, donde $\Sigma$ es un determinado alfabeto se denomina lenguaje.

1. El lenguaje de todas las cadenas que constan de $n$ ceros seguidos de $n$ unos para cualquier $n \ge 0$: $\{\varepsilon,01,0011,000111,...\}$.
2. $\Sigma^*$ es un lenguaje para cualquier alfabeto $\Sigma$.
3. $\emptyset$, el lenguaje vacío, es un lenguaje de cualquier alfabeto.
4. $\{\varepsilon \}$, el lenguaje que consta sólo de la cadena vacía, también es un lenguaje de cualquier alfabeto. *Observe que $\emptyset \neq \{\varepsilon\}$; el primero no contiene ninguna cadena y el segundo sólo tiene una cadena.*

Aunque los lenguajes pueden tener un número infinito de cadenas, están restringidos a que dichas cadenas estén formadas por los símbolos que definen un alfabeto finito y prefijado.

## Lenguaje Regular
Un leguaje $L$ es regular si existe una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $r$ define a $L$.

## Relaciones
Sea $L \subseteq \Sigma^*,\; x,y \in \Sigma^*$  entonces, $$x R_{L} y \iff \forall z \in \Sigma^* \; (xz \in L \land yz \in L) \lor (xz \notin L \land yz \notin L)$$
Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ un [[Autómata Finito Determinista|AFD]] entonces, $$xR_My \iff \hat{\delta}(q_0, x) = \hat{\delta}(q_0, y)$$
*Observación: $|R_M|$ es equivalente a la cantidad de estados de $M$.*

*Observación: no necesariamente se cumple que $xR_Ly \implies xR_My$.
Sin embargo, si se cumple que $xR_My \implies xR_Ly$. Por ende,  $|R_L| \leq |R_M|$*

