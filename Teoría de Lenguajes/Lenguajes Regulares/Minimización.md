Dado un [[Autómata Finito Determinista|AFD]] $M=(Q, \Sigma, \delta, q_0, F)$ __COMPLETO__,[^1] obtendremos un *autómata finito determinado equivalente y mínimo* $M'=(Q', \Sigma, \delta', q'_0, F')$.

1. Si hay algún estado inalcanzable eliminarlo.
2. $(i=0)$ Marcar todos los estados *distinguibles*[^2] con la cadena vacía (es decir, todos los finales se pueden distinguir de los no finales).
3. $(i=i+1)$ Marcar como *distinguibles* $q$ y $q'$ si con algún $a \in \Sigma$ obtenemos que $\delta(q,a)$ es distinguible de $\delta(q',a)$.
4. Si en el paso anterior se han distinguido nuevos estados, volver.

[^1]: Un [[Autómata Finito]] es *completo* cuándo todas sus transiciones están definidas.
[^2]: Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ un AFD donde $p, q \in Q$, entonces decimos que $p$ *es distinguible de* $q$ si $\exists x \in \Sigma^\ast: \hat{\delta}(p, x) \in F \land \hat{\delta}(q,x) \notin F$.
