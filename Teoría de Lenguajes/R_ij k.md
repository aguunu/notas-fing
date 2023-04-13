$R_{ij}^k$ son las cadenas que parten del estado $i$ y terminan en el estado $j$ sin pasar por un estado mayor a $k$.

Paso Base,
1. $R_{ij}^0=\{a \in \Sigma: \delta(q_i, a) = q_j \}$ con $i \neq j$
2. $R_{ii}^0=\{a \in \Sigma: \delta(q_i, a) = q_i \} \cup \{ \varepsilon \}$

Paso Inductivo,
1. $R_{ij}^k=R_{ij}^{k-1} \bigcup R_{ik}^{k-1} \cdot (R_{kk}^{k-1})^\star \cdot R_{kj}^{k-1}$

*Observación: expresando el $R_{ij}^k$ como una [[Expresiones Regulares|Expresión Regular]] obtenemos que,
$$R_{ij}^k=R_{ij}^{k-1} | R_{ik}^{k-1} \cdot (R_{kk}^{k-1})^\star \cdot R_{kj}^{k-1}$$

*Observación: Sea $F=\{f_1,...,f_m\}$ el conjunto de estados finales $\implies \bigcup_{j=1}^{m} R_{1 f_j}^m$ es el conjunto de cadenas aceptadas por el lenguaje.*
