Un *autómata finito no determinista* (AFN) tiene la capacidad de estar en varios estados a la vez.

Definimos un *autónoma finito no determinista* como $M=(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\delta : Q \times \Sigma \rightarrow 2^Q$ la función de transición.
- $q_0 \in Q$ el estado inicial.
- $F \subseteq Q$ el conjunto de estados finales.

Extendemos inductivamente la función de transición $\delta$ para que el autómata sea capaz de procesar cadenas de $\Sigma^\ast$,  con lo cual obtenemos $\hat{\delta} : Q \times \Sigma^\ast \rightarrow 2^Q$ definida de la siguiente manera:

$$
\forall q \in Q : \tilde{\delta}(q, \varepsilon) = \{q\}
$$

$$
\forall q \in Q, \forall a \in \Sigma, \forall x \in \Sigma^\ast : \hat{\delta}(q, xa) = \tilde{\delta}(\hat{\delta}(q, x), a) \text{ donde } \tilde{\delta} : 2^Q \times \rightarrow 2^Q \mid \tilde{\delta}(P, a) = \bigcup_{q \in P}\delta(q, a)
$$

>[!important] Lenguaje Aceptado
>Dado un AFN-$\varepsilon$ $M=(Q,\Sigma,\delta, q_0, F)$  $\implies$  $L(M) = \{ x \in \Sigma^\ast : \hat{\delta}(q_0, x) \cap F \neq \emptyset \}$

>[!important] Lenguaje Regular
>Si $L$ es aceptado por algún AFN $\implies$ $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]].

## AFN $\rightarrow$ AFD
Dado un AFN $M=(Q,\Sigma,\delta, q_0, F)$ construiremos un [[Autómata Finito Determinista|AFD]] $M=(Q', \Sigma, \delta', q_0, F')$.

1. $F'=Q'=\emptyset$
1. $P=\{\{q_0\}\}$.
2. Mientras $P \neq \emptyset$
	1. Elegir y remover un conjunto de estados arbitrario $S$ de $P$.
	2. $\forall a \in \Sigma$
		1. $S'=\bigcup_{q \in S}\delta(q, a)$
		2. Llamemos $q$ a un nuevo estado identificado a partir del conjunto $S'$.
		3. Si $q \notin Q' \rightarrow$ Agregar $q$ a $Q'$, a su vez agregar $S'$ a $P$.
		4. Si $\exists f \in F : f \in S' \rightarrow$ Agregar $q$ a $F'$.
		5. $\delta'(S,a)=q$ donde $q$ es el estado agregado en el paso anterior.
