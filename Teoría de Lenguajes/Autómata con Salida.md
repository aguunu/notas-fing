## Máquina de Mealy
Una *máquina de Mealy* es un *autómata con salida* cuya salida depende tanto del estado actual como de la entrada actual.

Definimos una *máquina de Mealy* como $M=(Q, \Sigma, \Delta, \delta, \lambda, q_0)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\Delta$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de salida.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $\lambda : Q \times \Sigma \rightarrow \Delta$ la función de salida.
- $q_0 \in Q$ el estado inicial.

Extendiendo la función $\delta : Q \times \Sigma \rightarrow Q$:
- $\hat{\delta}: Q \times \Sigma^{\star} \rightarrow Q$
- $\hat{\delta}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\star}$

Extendiendo la función $\lambda : Q \times \Sigma \rightarrow \Delta$
- $\hat{\lambda} : Q \times \Sigma^{\star} \rightarrow \Delta^{\star}$
- $\hat{\lambda}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\lambda}(q, wa) = \hat{\lambda}(q, w) \cdot \lambda(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\star}$

## Máquina de Moore
Una *máquina de Moore* es un *autómata con salida* cuya salida depende únicamente del estado actual.

Definimos una *máquina de Moore* como una $M = (Q, \Sigma, \Delta, \delta, \lambda, q_0)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\Delta$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de salida.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $\lambda : Q \rightarrow \Delta$ la función de salida.
- $q_0 \in Q$ el estado inicial.

Extendiendo la función $\delta$:
- $\hat{\delta} : Q \times \Sigma^{\star} \rightarrow Q$
- $\hat{\delta}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\star}$

Extendiendo la función $\lambda$:
- $\hat{\lambda}: Q \times \ \Sigma^{\star} \rightarrow \Delta^{\star}$
- $\hat{\lambda}(q, \varepsilon) = \varepsilon \; \forall q \in Q$
- $\hat{\lambda}(q, wa) = \hat{\lambda}(q, w) \cdot \hat{\lambda}(\hat{\delta}(q, wa)) \; \forall q \ in Q, a \in \Sigma, w \in \Sigma^{\star}$