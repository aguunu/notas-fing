Un autómata finito no determinista con transición-$\varepsilon$ (AFND-$\varepsilon$) permite transiciones para $\epsilon$, la cadena vacía. Así, un AFN puede hacer una transición espontáneamente, sin recibir un símbolo de entrada.

Se define la clausura $\varepsilon \text{-} clausura(q)$ como el conjunto de estados a los que se pueden llegar partiendo desde $q$ utilizando únicamente arcos $\varepsilon$.
Algunas propiedades que cumple el $\varepsilon\text{-}clausura$:
- $q \in \varepsilon \text{-}clausura(q)$
- $\varepsilon \text{-}clausura(\varepsilon \text{-}clausura(q)) = \varepsilon \text{-}clausura(q)$
- $\varepsilon \text{-}clausura(Q) = \bigcup_{q \in Q}\varepsilon \text{-}clausura(q)$

Definimos un AFND-$\varepsilon$ como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un  [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\delta : Q \times (\Sigma \cup \{ \varepsilon \}) \rightarrow 2^Q$ la función de transición.
- $q_0$ un estado inicial donde $q_0 \in Q$.
- $F$ un conjunto de estados finales con $F \subseteq Q$.

Un lenguaje $L$ es aceptado por algún AFN-$\varepsilon$ si y sólo si $L$ es aceptado por algún AFD.

## AFND-$\varepsilon$ $\rightarrow$ AFND
1. Para todo estado $q$ del AFND-$\varepsilon$,
	1. Hallar $\varepsilon \text{-}cl(q)$, el conjunto de estados a los que se pueden llegar partiendo desde $q$ utilizando únicamente arcos $\varepsilon$.
	2. Hallar $\tilde{\delta}(\varepsilon \text{-}cl(q), a)$ el conjunto de todos los estados que parten de algún estado de la clausura de $q$ y consumen el símbolo $a$.
	3. Hallar $\delta'(q,a)=\varepsilon \text{-}cl(\tilde{\delta}(\varepsilon \text{-}cl(q), a))$, la clausura del conjunto obtenido en el paso anterior. *En otras palabras, todos los estados de los que se puede llegar partiendo desde $q$ consumiendo una única vez el símbolo $a$ y arcos $\varepsilon$.*

*Observación: se recomienda calcular la clausura de cada estado antes de empezar a iterar en el algoritmo.*