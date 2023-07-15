Un *autómata finito determinista (AFD)* es un [[Autómata Finito|AF]] que sólo puede estar en un único estado después de leer cualquier secuencia de entradas.

Definimos un *AFD* como $M=(Q,\Sigma,\delta, q_0, F)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\delta : Q \times \Sigma \rightarrow Q$ la función de transición.
- $q_0 \in Q$ el estado inicial.
- $F \subseteq Q$ el conjunto de estados finales.

Extendemos inductivamente la función de transición $\delta$ para que el autómata sea capaz de procesar cadenas de $\Sigma^\ast$,  con lo cual obtenemos $\hat{\delta} : Q \times \Sigma^\ast \rightarrow Q$ definida de la siguiente manera:

$$
\tag{1} \forall q \in Q : \hat{\delta}(q, \varepsilon) = q
$$

$$
\tag{2} \forall q \in Q, \forall a \in \Sigma, \forall x \in \Sigma^\ast : \hat{\delta}(q, xa) = \delta(\hat{\delta}(q, x), a)
$$

## Lenguaje Aceptado
Sea $M=(Q,\Sigma,\delta, q_0, F)$ un [[Autómata Finito Determinista]] entonces,

$$\tag{Lenguaje Aceptado} \mathscr{L}(M) = \{ x \in \Sigma^\ast : \hat{\delta}(q_0, x) \in F \}$$

>[!important]
>Si $L$ es aceptado por algún AFD $\implies$ $L$ es un [[Lenguaje Regular]].

## AFD $\rightarrow$ Expresión Regular
Dado un AFD $M$ se quiere hallar una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $\mathscr{L}(M)$ = $\mathscr{L}(r)$.
Para esto podemos utilizar cualquiera de los siguientes métodos:
- [[Lenguaje Restringido]]
- [[Clases de Equivalencia]]
- [[Análisis de Kleene]]
