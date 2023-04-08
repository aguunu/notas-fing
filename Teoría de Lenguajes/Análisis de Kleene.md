Dado un [[Autómata Finito Determinista|AFD]] $M$ se quiere hallar una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $L(M)$ = $L(r)$.

## Aplicación
1. Plantear un sistema de ecuaciones con una variable $X_i$ por cada estado. *Cada variable $X_i$ representa "¿Qué forma tengo de llegar a un estado final desde $q_i$?"*
2. A cada $X$ que este asociada a un estado final agregarle $\varepsilon$.
3. Las $X_i$ se forman con las transiciones salientes.
4. La expresión regular $r$ buscada será la asociada al estado inicial.

*Observación: se utiliza el [[#Lema Arden]] para resolver ecuaciones donde $X=rX|s$.*

*Observación: no incluir el estado pozo facilita las cuentas (la solución del estado pozo siempre es la misma $X_p=\emptyset$).*

## Lema Arden
Nos permite afirmar que $X=r^* \cdot s$ es la solución a la ecuación $X=rX|s$ donde $\varepsilon \notin L(r)$.