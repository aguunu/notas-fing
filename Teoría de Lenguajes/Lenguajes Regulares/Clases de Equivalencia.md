Las *clases de equivalencia* de un [[Autómata Finito Determinista|AFD]] nos dan las [[Expresiones Regulares|Expresiones Regulares]] que generan las cadenas de las distintas clases de $R_M$.

Por lo tanto, dado un [[Autómata Finito Determinista|AFD]] $M$, la [[Expresiones Regulares|Expresiones Regulares]] $r : \mathscr{L}(r) = \mathscr{L}(M)$ puede hallarse a través de las clases de equivalencia. Pues $r=X_{f_1}|...|X_{f_m}$ donde $X_f$ son las clases de equivalencia asociadas a los estados finales de $M$.

Hallar las *clases de equivalencia* de $R_M$:
1. Plantear un sistema de ecuaciones con una variable $X_i$ por cada estado. *Cada variable $X_i$ representa "¿Qué forma tienen las cadenas que terminan en $q_i$?"*.
2. A la variable $X$ que este asociada al estado inicial se le agrega $\varepsilon$.
3. Hallar la solución al sistema planteado, es decir, hallar la solución correspondiente a cada variable $X_i$.

>[!note] Lema Arden II 
>$X=s \cdot r^\ast$ es solución a la ecuación $X=Xr|s$ donde $\varepsilon \notin \mathscr{L}(r)$.

>[!warning]
 Se deberá incluir el "estado pozo" ya que este define una clase de equivalencia.

>[!important] 
>Si el autónoma $M$ es __MÍNIMO__ y __COMPLETO__, entonces, $R_M = R_L$.
