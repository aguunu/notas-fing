Una *máquina de Moore* es un [[Autómata Con Salida]] cuya salida depende únicamente del estado actual.

Definimos una *máquina de Moore* como una $M = (Q, \Sigma, \Delta, \delta, \lambda, q_0)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\Delta$ un [[Alfabeto]] de salida.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $\lambda : Q \rightarrow \Delta$ la función de salida.
- $q_0 \in Q$ el estado inicial.

Extendiendo la función $\delta$:
- $\hat{\delta} : Q \times \Sigma^{\ast} \rightarrow Q$
- $\hat{\delta}(q, \varepsilon) = q \; \forall q \in Q$
- $\hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a) \; \forall q \in Q, a \in \Sigma, w \in \Sigma^{\ast}$

Extendiendo la función $\lambda$:
- $\hat{\lambda}: Q \times \ \Sigma^{\ast} \rightarrow \Delta^{\ast}$
- $\hat{\lambda}(q, \varepsilon) = \varepsilon \; \forall q \in Q$
- $\hat{\lambda}(q, wa) = \hat{\lambda}(q, w) \cdot \hat{\lambda}(\hat{\delta}(q, wa)) \; \forall q \ in Q, a \in \Sigma, w \in \Sigma^{\ast}$
