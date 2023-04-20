Las *clases de equivalencia* de un AFD nos dan las [[Expresiones Regulares|Expresiones Regulares]] que generan las cadenas de las distintas clases de $R_M$.

Por lo tanto, dado un [[Autómata Finito Determinista|AFD]] $M$, la [[Expresiones Regulares|Expresión Regular]] $r : L(M) = L(r)$ puede hallarse a través de las clases de equivalencia. Pues $r=X_{f_1}|...|X_{f_m}$ donde $X_f$ son las clases de equivalencia asociadas a los estados finales de $M$.

Hallar las clases de equivalencia de $R_M$:
1. Plantear un sistema de ecuaciones con una variable $X_i$ por cada estado. *Cada variable $X_i$ representa "¿Qué forma tienen las cadenas que terminan en $q_i$?"*
2. A la variable $X$ que este asociada al estado inicial se le agrega $\varepsilon$.
3. Hallar la solución al sistema planteado, es decir, hallar la solución correspondiente a cada variable $X_i$.

>[!tip] 
Si el autónoma $M$ es mínimo y completo (todas sus transiciones están definidas), las clases de equivalencia de $R_M$ calculadas coinciden con las de $R_L$

>[!note] Lema Arden II
>Para resolver las ecuaciones de la forma $X=Xr|s$ se utiliza el *lema arden*. Que nos permite afirmar que $X=s \cdot r^\star$ es la solución a la ecuación $X=Xr|s$ donde $\varepsilon \notin L(r)$.

>[!warning] ¡Cuidado!
 A diferencia del [[Análisis de Kleene]], se deberá incluir el estado pozo ya que este define una clase de equivalencia.