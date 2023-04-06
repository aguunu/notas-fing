Dado un [[Autómatas#Autómata Finito Determinista|AFD]] $M$ se quiere hallar una [[Expresiones Regulares|expresión regular]] $r$ tal que $L(M)$ = $L(r)$.
*Esté método calcula las clases de equivalencia de $R_M$.*

## Aplicación
1. Plantear un sistema de ecuaciones con una variable $Y_i$ por cada estado. *Cada variable $Y_i$ representa "¿Qué forma tienen las cadenas que terminan en $q_i$?"*
2. A $Y$ que este asociada al estado inicial se le agrega $\varepsilon$.
3. Las $X_i$ se forman con las transiciones entrantes.
4. Sea $F= \{q_{f_1}, ..., q_{f_m}\}$, entonces la expresión regular $r$ es $r=Y_{f_1}|...|Y_{f_m}$

*Observación: se utiliza el [[Análisis de Kleene#Lema Arden|Lema Arden]] para resolver ecuaciones donde $X=rX|s$.*

*Observación: a diferencia del [[Análisis de Kleene]], se deberá incluir el estado pozo ya que este define una clase de equivalencia.*

*Observación: si el autónoma $M$ es mínimo y completo (todas sus transiciones están definidas), las clases de equivalencia de $R_M$ calculadas coinciden con las de $R_L$*