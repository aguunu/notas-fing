Un *autómata finito no determinista con transición-$\varepsilon$ (AFN-$\varepsilon$)* es una variante del [[Autómata Finito No-Determinista|AFN]] que permite transiciones para la [[Cadena de Caracteres#Cadena Vacía $ varepsilon$|Cadena Vacía]] $\varepsilon$. Así, un [[Autómata Finito No-Determinista|AFN]] puede hacer una transición espontáneamente, sin consumir el símbolo de entrada.

Definimos un *AFN-$\varepsilon$* como $M=(Q,\Sigma,\delta, q_0, F)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\delta : Q \times (\Sigma \cup \{ \varepsilon \}) \rightarrow 2^Q$ la función de transición.
- $q_0 \in Q$ el estado inicial.
- $F \subseteq Q$ el conjunto de estados finales.

Extendemos inductivamente la función de transición $\delta$ para que el autómata sea capaz de procesar cadenas de $\Sigma^\ast$, con lo cual obtenemos $\hat{\delta} : Q \times \Sigma^\ast \rightarrow 2^Q$ definida de la siguiente manera:

$$
\forall q \in Q : \hat{\delta}(q, \varepsilon) = \varepsilon \text{-}cl(q)
$$

$$
\forall q \in Q, \forall a \in \Sigma, \forall x \in \Sigma^\ast : \hat{\delta}(q, xa) = \varepsilon \text{-}cl(\tilde{\delta}(\hat{\delta}(q,x),a)) \text{ donde } \tilde{\delta} : 2^Q \times \Sigma \rightarrow 2^Q \mid \tilde{\delta}(P, a) = \bigcup_{q \in P}\delta(q, a)
$$

## $\varepsilon \text{-} clausura(q)$
Se define la clausura $\varepsilon \text{-} cl(q) : Q \rightarrow 2^Q$ como el conjunto de estados a los que se pueden llegar partiendo desde $q$ utilizando únicamente arcos $\varepsilon$. Observar que se cumplen las siguientes propiedades para un AFN-$\varepsilon$ arbitrario:
- $\forall q \in Q : q \in \varepsilon \text{-}cl(q)$
- $\forall q \in Q : \varepsilon \text{-}cl(\varepsilon \text{-}cl(q)) = \varepsilon \text{-}cl(q)$
- $\forall P \subseteq Q : \varepsilon \text{-}cl(P) = \bigcup_{q \in P}\varepsilon \text{-}cl(q)$

>[!important] Lenguaje Aceptado
>Dado un AFN-$\varepsilon$ $M=(Q,\Sigma,\delta, q_0, F)$  $\implies$  $L(M) = \{ x \in \Sigma^\ast : \hat{\delta}(q_0, x) \cap F \neq \emptyset \}$

>[!important] Lenguaje Regular
>Si $L$ es aceptado por algún AFN-$\varepsilon$ $\implies$ $L$ es un [[Expresiones Regulares|Lenguaje Regular]].

## AFN-$\varepsilon$ $\rightarrow$ AFN
Dado un AFN-$\varepsilon$  $M=(Q,\Sigma,\delta, q_0, F)$ construiremos un [[Autómata Finito No-Determinista|AFN]] $M=(Q', \Sigma, \delta', q_0, F')$.

1. $Q'=Q$
2.  $\forall q \in Q, \forall a \in \Sigma$
	1. Hallar $\varepsilon \text{-}cl(\tilde{\delta}(\varepsilon \text{-}cl(q), a))$. *Es decir, todos los estados de los que se puede llegar partiendo desde $q$ consumiendo arcos $\varepsilon$ y una única vez el símbolo $a$.*
	2. $\delta'(q, a) = c$ donde $c$ es el conjunto hallado en la parte anterior.
3. $F'=\begin{cases}F \cup \{q_0\},  & \text{si } \varepsilon \text{-}cl(q_0) \cap F \neq \emptyset \\F, & \text{en otro caso}\end{cases}$
4. Eliminar los estados sin transiciones entrantes y las transiciones salientes de dichos estados.

>[!info] 
> Se recomienda calcular la clausura de cada estado antes de empezar a iterar en el algoritmo.
