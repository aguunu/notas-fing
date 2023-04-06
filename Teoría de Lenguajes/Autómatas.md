## Autómata Finito Determinista
Un autómata finito determinista (AFD) sólo puede estar en un único estado después de leer cualquier secuencia de entradas.

Definimos un AFD como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados
- $\Sigma$ un conjunto de los símbolos de entrada
- $\delta : Q \times \Sigma \rightarrow Q$ una función de transición, que toma como entrada un estado y una entrada y retorna un estado.
- $q_0$ un estado inicial, perteneciente a $Q$.
- $F$ un conjunto de estados finales.

### Lenguaje de un AFD
Definimos el lenguaje de un AFD $A=(Q,\Sigma,\delta, q_0, F)$ como $L(A)=\{w : \hat{\delta}(q_0, w) \in F\}$ donde $\delta$ se define inductivamente,
1. $\hat{\delta}(q, \varepsilon) = q$
2. $\hat{\delta}(q, xa) = \delta(\hat{\delta}(q, x), a)$

El lenguaje $L(A)$ es el conjunto de cadenas $w$ que parten del estado inicial $q_0$ y van hasta uno de los estados de aceptación.

Si $L$ es $L(A)$ para un determinado AFD $A$, entonces $L$ es un [[Conceptos Fundamentales#^6942bd|Lenguaje Regular]].

## Autómata Finito No Determinista
Un autómata finito “no determinista” (AFN) tiene la capacidad de estar en varios estados a la vez. Esta capacidad a menudo se expresa como la posibilidad de que el autómata “conjeture” algo acerca de su entrada.

Definimos un AFD como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados
- $\Sigma$ un conjunto de los símbolos de entrada
- $\delta : Q \times \Sigma \rightarrow 2^Q$ una función de transición, que toma como entrada un estado y una entrada y retorna un conjunto estados.
- $q_0$ un estado inicial, perteneciente a $Q$.
- $F$ un conjunto de estados finales.

*Observación: la única diferencia entre un AFN y un AFD se encuentra en el tipo de valor que devuelve $\delta$: un conjunto de estados en el caso de un AFN y un único estado en el caso de un AFD.*

### Lenguaje de un AFN
Definimos el lenguaje de un AFN $A=(Q,\Sigma,\delta, q_0, F)$ como $L(A)=\{w:\hat{\delta}(q_0,w) \cup F \neq \emptyset \}$ donde $\delta$ se define inductivamente,
1. $\hat{\delta}(q, \varepsilon) = q$
2. $\hat{\delta}(q, xa) = \bigcup_{i = 1}^{k} \delta(p_i, a)$ donde $\hat{\delta}(q,x)=\{p_1,p_2,...,p_k\}$ 

El lenguaje $L(A)$ es el conjunto de cadenas $w \in \Sigma^*$ tal que $\delta(q_o, w)$ contiene al menos un estado de aceptación.

## Autómata Finito No Determinista con Transición-$\varepsilon$
Un autómata finito no determinista con transición-$\varepsilon$ (AFND-$\varepsilon$) permite transiciones para ε, la cadena vacía. Así, un AFN puede hacer una transición espontáneamente, sin recibir un símbolo de entrada.

Se define la clausura $\varepsilon \text{-} clausura(q)$ como el conjunto de estados a los que se pueden llegar partiendo desde $q$ utilizando únicamente arcos $\varepsilon$.

- $q \in \varepsilon \text{-}clausura(q)$
- $\varepsilon \text{-}clausura(\varepsilon \text{-}clausura(q)) = \varepsilon \text{-}clausura(q)$
- $\varepsilon \text{-}clausura(Q) = \bigcup_{q \in Q}\varepsilon \text{-}clausura(q)$

Definimos un AFND-$\varepsilon$ como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados
- $\Sigma$ un conjunto de los símbolos de entrada
- $\delta : Q \times (\Sigma \cup \{ \varepsilon \}) \rightarrow 2^Q$ una función de transición, que toma como entrada un estado y una entrada y retorna un conjunto estados.
- $q_0$ un estado inicial, perteneciente a $Q$.
- $F$ un conjunto de estados finales.

Un lenguaje $L$ es aceptado por algún AFN-$\varepsilon$ si y sólo si $L$ es aceptado por algún AFD.

## AFND-$\varepsilon$ $\rightarrow$ AFND
1. Para todo estado $q$ del AFND-$\varepsilon$,
	1. Hallar $\varepsilon \text{-}cl(q)$, el conjunto de estados a los que se pueden llegar partiendo desde $q$ utilizando únicamente arcos $\varepsilon$.
	2. Hallar $\tilde{\delta}(\varepsilon \text{-}cl(q), a)$ el conjunto de todos los estados que parten de algún estado de la clausura de $q$ y consumen el símbolo $a$.
	3. Hallar $\delta'(q,a)=\varepsilon \text{-}cl(\tilde{\delta}(\varepsilon \text{-}cl(q), a))$, la clausura del conjunto obtenido en el paso anterior. *En otras palabras, todos los estados de los que se puede llegar partiendo desde $q$ consumiendo una única vez el símbolo $a$ y arcos $\varepsilon$.*

*Observación: se recomienda calcular la clausura de cada estado antes de empezar a iterar en el algoritmo.*

## AFND $\rightarrow$ AFD
TODO

## RE $\rightarrow$ AFND-$\varepsilon$
TODO

## AFD $\rightarrow$ RE
- [[R_ij k]]
- [[Análisis de Kleene]]
- [[Clases de Equivalencia]]