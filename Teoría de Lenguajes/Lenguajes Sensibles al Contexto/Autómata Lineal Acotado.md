Un *autómata lineal acotado (ALA)* es un caso particular de una [[Máquina de Turing]], el cual permite computar todos los [[Lenguaje Sensible al Contexto|Lenguajes Sensibles al Contexto]]. La diferencia con una [[Máquina de Turing]] es que cadena a ser analizada se encuentra entre los símbolos $\cancel{c}$ y $\cancel{s}$. Por ende, las operaciones que se pueden aplicar están restringidas al rango delimitado por estos símbolos. Por lo tanto, estos símbolos no podrán ser sobrescritos.

Se define un *autómata lineal acotado (ALA)* como $M=(Q, \Sigma, \Gamma, \delta, q_0, \cancel{c}, \cancel{s}, F)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma \in \Gamma$ un [[Alfabeto]] de entrada.
- $\Gamma$ el [[Alfabeto]] de la *cinta*.
- $\delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \{I, D\}$ la función de transición. 
- $\cancel{c}$ el símbolo delimitador del *origen* de la entrada.
- $\cancel{s}$ el símbolo delimitador del *final* de la entrada.
- $F \subseteq Q$ el conjunto **unitario** de estados finales, para el cual $\delta$ esta *indefinida*.

>[!warning] 
>Las transiciones que involucren el símbolo $\cancel{c}$ deberán ser de la forma $\delta(q, \cancel{c})=(p, \cancel{c}, D) \; \forall q,p \in \Sigma$. De forma análoga para el símbolo $\cancel{s}$ deberán ser de la forma $\delta(q, \cancel{s})=(p, \cancel{s}, I) \; \forall q,p \in \Sigma$.

>[!important] 
>Un [[Lenguaje]] $L$ es un [[Lenguaje Sensible al Contexto]] si es aceptado por algún [[Autómata Lineal Acotado]].
