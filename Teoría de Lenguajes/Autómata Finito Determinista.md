Un *autómata finito determinista (AFD)* sólo puede estar en un único estado después de leer cualquier secuencia de entradas.

Definimos un *AFD* como $M=(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Conceptos Fundamentales#Alfabetos|Alfabeto]] de entrada.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $q_0 \in Q$ el estado inicial.
- $F \subseteq Q$ el conjunto de estados finales.

Extendemos inductivamente la función de transición $\delta$ para que el autómata sea capaz de procesar cadenas de $\Sigma^\ast$,  con lo cual obtenemos $\hat{\delta} : Q \times \Sigma^\ast \rightarrow Q$ definida de la siguiente manera:
$$
\forall q \in Q : \hat{\delta}(q, \varepsilon) = q
$$
$$
\forall q \in Q, \forall a \in \Sigma, \forall x \in \Sigma^\ast : \hat{\delta}(q, xa) = \delta(\hat{\delta}(q, x), a)
$$

>[!important] Lenguaje Aceptado
>Dado un AFD $M=(Q,\Sigma,\delta, q_0, F)$  $\implies$  $L(M) = \{ x \in \Sigma^\ast : \hat{\delta}(q_0, x) \in F \}$

>[!important] Lenguaje Regular
>Si $L$ es aceptado por algún AFN $\implies$ $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]].

El lenguaje $L(A)$ es el conjunto de cadenas $w$ que parten del estado inicial $q_0$ y van hasta uno de los estados de aceptación.

Si $L$ es $L(A)$ para un determinado AFD $A$, entonces $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]].

## AFD $\rightarrow$ Expresión Regular
Dado un AFD $M$ se quiere hallar una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $L(M)$ = $L(r)$.
Para esto tenemos 3 métodos distintos:
- [[Lenguaje Restringido en AFD]]
- [[Clases de Equivalencia]]
- [[Análisis de Kleene]]