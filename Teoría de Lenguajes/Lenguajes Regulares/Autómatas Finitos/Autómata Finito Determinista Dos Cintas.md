Un *autómata finito determinista de dos cintas (AFD dos cintas)* es una variante de [[Autómata Finito Determinista|AFD]], que posee dos cintas independientes. A diferencia del [[Autómata Con Salida]], ambas cintas son de entrada.

Definimos un *AFD de dos cintas* como $M=(Q_1, Q_2, \Sigma,\delta, q_0, F)$ donde,
- $Q_1$ un conjunto finito de estados que avanzan sobre la cinta #1.
- $Q_2$ un conjunto finito de estados que avanzan sobre la cinta #2.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\delta : (Q_1 \cup Q_2) \times \Sigma \rightarrow (Q_1 \cup Q_2)$ la función de transición.
- $q_0 \in (Q_1 \cup Q_2)$ el estado inicial.
- $F \subseteq (Q_1 \cup Q_2)$ el conjunto de estados finales.

## Lenguaje Aceptado
Sea $M=(Q_1, Q_2, \Sigma, \delta, q_0, F)$ un AFD de Dos Cintas, el *lenguaje aceptado por $M$*,
$$\tag{Lenguaje Aceptado} \mathscr{L}(M)=\{(x,y) \in \Sigma^\star \times \Sigma^\star : \hat{\delta}(q_0, x, y) \in F \}$$