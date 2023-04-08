Un autómata finito determinista (AFD) sólo puede estar en un único estado después de leer cualquier secuencia de entradas.

Definimos un AFD como una "quíntupla" $(Q,\Sigma,\delta, q_0, F)$ donde:
- $Q$ un conjunto finito de estados
- $\Sigma$ un conjunto de los símbolos de entrada
- $\delta : Q \times \Sigma \rightarrow Q$ una función de transición, que toma como entrada un estado y una entrada y retorna un estado.
- $q_0$ un estado inicial, perteneciente a $Q$.
- $F$ un conjunto de estados finales.

## Lenguaje de un AFD
Definimos el lenguaje de un AFD $A=(Q,\Sigma,\delta, q_0, F)$ como $L(A)=\{w : \hat{\delta}(q_0, w) \in F\}$ donde $\delta$ se define inductivamente,
1. $\hat{\delta}(q, \varepsilon) = q$
2. $\hat{\delta}(q, xa) = \delta(\hat{\delta}(q, x), a)$

El lenguaje $L(A)$ es el conjunto de cadenas $w$ que parten del estado inicial $q_0$ y van hasta uno de los estados de aceptación.

Si $L$ es $L(A)$ para un determinado AFD $A$, entonces $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]].

## ADF $\rightarrow$ Expresión Regular
Dado un AFD $M$ se quiere hallar una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $L(M)$ = $L(r)$.
Para esto tenemos 3 métodos distintos:
- [[R_ij k]]
- [[Clases de Equivalencia]]
- [[Análisis de Kleene]]