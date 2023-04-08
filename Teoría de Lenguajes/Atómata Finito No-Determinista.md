Un autómata finito “no determinista” (AFN) tiene la capacidad de estar en varios estados a la vez. Esta capacidad a menudo se expresa como la posibilidad de que el autómata “conjeture” algo acerca de su entrada.

Definimos un AFD como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados
- $\Sigma$ un conjunto de los símbolos de entrada
- $\delta : Q \times \Sigma \rightarrow 2^Q$ una función de transición, que toma como entrada un estado y una entrada y retorna un conjunto estados.
- $q_0$ un estado inicial, perteneciente a $Q$.
- $F$ un conjunto de estados finales.

*Observación: la única diferencia entre un AFN y un AFD se encuentra en el tipo de valor que devuelve $\delta$: un conjunto de estados en el caso de un AFN y un único estado en el caso de un AFD.*

## Lenguaje de un AFN
Definimos el lenguaje de un AFN $A=(Q,\Sigma,\delta, q_0, F)$ como $L(A)=\{w:\hat{\delta}(q_0,w) \cup F \neq \emptyset \}$ donde $\delta$ se define inductivamente,
1. $\hat{\delta}(q, \varepsilon) = q$
2. $\hat{\delta}(q, xa) = \bigcup_{i = 1}^{k} \delta(p_i, a)$ donde $\hat{\delta}(q,x)=\{p_1,p_2,...,p_k\}$ 

El lenguaje $L(A)$ es el conjunto de cadenas $w \in \Sigma^*$ tal que $\delta(q_o, w)$ contiene al menos un estado de aceptación.

## AFN $\rightarrow$ AFD
TODO