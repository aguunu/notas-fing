Un *autómata finito determinista de dos cintas (AFD de dos cintas)* es una variante de [[Autómata Finito Determinista|AFD]], que posee dos cintas independientes. La diferencia con un [[Autómatas Con Salida]] es que en este caso, ambas cintas son de entrada.

Definimos un *AFD de dos cintas* como $M=(Q_1, Q_2, \Sigma,\delta, q_0, F)$ donde:
- $Q_1$ un conjunto finito de estados que avanzan sobre la cinta #1.
- $Q_2$ un conjunto finito de estados que avanzan sobre la cinta #2.
- $\Sigma$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\delta : (Q_1 \cup Q_2) \times \Sigma \rightarrow (Q_1 \cup Q_2)$ la función de transición.
- $q_0 \in (Q_1 \cup Q_2)$ el estado inicial.
- $F \subseteq (Q_1 \cup Q_2)$ el conjunto de estados finales.