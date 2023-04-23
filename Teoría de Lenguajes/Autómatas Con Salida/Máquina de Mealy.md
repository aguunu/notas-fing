Una *máquina de Mealy* es un [[Autómata Con Salida]] cuya salida depende tanto del estado actual como de la entrada actual.

Definimos una *máquina de Mealy* como $M=(Q, \Sigma, \Delta, \delta, \lambda, q_0)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\Delta$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de salida.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $\lambda : Q \times \textcolor{red}{\Sigma} \rightarrow \Delta$ la función de salida.[^1]
- $q_0 \in Q$ el estado inicial.

Extendiendo la función $\delta : Q \times \Sigma \rightarrow Q$:
- $\hat{\delta}: Q \times \Sigma^{\ast} \rightarrow Q$
- $\hat{\delta}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\ast}$

Extendiendo la función $\lambda : Q \times \Sigma \rightarrow \Delta$
- $\hat{\lambda} : Q \times \Sigma^{\ast} \rightarrow \Delta^{\ast}$
- $\hat{\lambda}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\lambda}(q, wa) = \hat{\lambda}(q, w) \cdot \lambda(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\ast}$

[^1]: A diferencia con la [[Máquina de Moore]], la función de salida $\lambda$ de *Mealy* además del estado actual, también depende de la entrada actual. 
