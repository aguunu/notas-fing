Es un modelo donde dispondremos de una cantidad finita de estados junto con una cinta  infinita sobre la cual podremos movernos a la izquierda o hacia la derecha tantas veces como sea necesario, así como leer y escribirla donde queramos.

>[!warning] 
>Nos restringiremos a las *máquinas de Turing* deterministas, de una cinta y con un solo estado de aceptación del cual no salen transiciones (de modo que, al llegar a este, la máquina se detenga).

Se define una *máquina de Turing (MT)* como $M=(Q, \Sigma, \Gamma, \delta, q_0, \cancel{b}, F)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma \in \Gamma$ un [[Alfabeto]] de entrada.
- $\Gamma$ el [[Alfabeto]] de la *cinta*.
- $\delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \{I, D\}$ la función de transición. 
- $q_0 \in Q$ el estado inicial.
- $\cancel{b}$ un símbolo que representa que la celda de la *cinta* está vacía.
- $F \subseteq Q$ el conjunto **unitario** de estados finales, para el cual $\delta$ esta *indefinida*.

>[!info] 
>Asumimos que la *cinta* se inicia con el cabezal de lectura/escritura sobre el primer símbolo de la tira que se da como entrada.

## Lenguaje Aceptado

Dada una *MT* $M=(Q, \Sigma, \Gamma, \delta, q_0, \cancel{b}, F)$, entonces, el lenguaje aceptado por $M$ es $$L(M)=\{x \in \Sigma^\star \mid M \textit{ llega a $q_f$ $\in$ F con x como entrada. }\}$$

## Lenguaje Recursivamente Enumerable
Un lenguaje $L$ es *recursivamente enumerable* si es aceptado por alguna [[Máquina de Turing]].
