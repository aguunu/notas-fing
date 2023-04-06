>$\text{Sea }L \subseteq \Sigma^*, \; x,y \in \Sigma^* \implies x R_{L} y \iff \forall z \in \Sigma^* \; (xz \in L \land yz \in L) \lor (xz \notin L \land yz \notin L)$

> $\text{Sea } M=\{Q, \Sigma, \delta, q_0, F\}$ un [[Autómatas#Autómata Finito Determinista|AFD]] $\implies$ $xR_My \iff \hat{\delta}(q_0, x) = \hat{\delta}(q_0, y)$

*Observación: $|R_M|$ es equivalente a la cantidad de estados de $M$.*

*Observación: no necesariamente se cumple que $xR_Ly \implies xR_My$.
Sin embargo, se cumple lo siguiente $xR_My \implies xR_Ly$. Por ende,  $|R_L| \leq |R_M|$*

## Estados
Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ y además  $p, q \in Q$:

- $p$ y $q$ son *estados equivalentes* si $\forall z \in \Sigma^* \hat{\delta}(p,z) = \hat{\delta}(q,z)$

- $p$ es *distinguible* de $q$ si $\exists x \in \Sigma^*: (\hat{\delta}(p, x) \in F) \land (\hat{\delta}(q,x) \notin F)$ 

