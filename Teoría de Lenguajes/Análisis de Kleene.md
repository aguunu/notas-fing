Dado un [[Autómata Finito Determinista|AFD]] $M$ se quiere hallar una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $L(M)$ = $L(r)$.

Para realizar el análisis de Kleene:
1. Plantear un sistema de ecuaciones con una variable $X_i$ por cada estado. *Cada variable $X_i$ representa "¿Qué forma tengo de llegar a un estado final desde $q_i$?"*
2. A cada $X$ que este asociada a un estado final agregarle $\varepsilon$.
3. La expresión regular $r$ buscada será la asociada al estado inicial.

>[!tip] Estado Pozo
>No incluir el estado pozo facilita las cuentas, pues la solución al estado pozo siempre es la misma $X_p = \emptyset$.

>[!note] Lema Arden I
>Para resolver las ecuaciones de la forma $X=rX|s$ se utiliza el *lema arden*. Que nos permite afirmar que $X=r^\ast \cdot s$ es la solución a la ecuación $X=rX|s$ donde $\varepsilon \notin L(r)$.
