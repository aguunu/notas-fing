Dado un [[Autómata Finito Determinista|AFD]] $M=(Q, \Sigma, \delta, \textcolor{yellow}{q_1}, F)$ con $Q=\{\textcolor{yellow}{q_1},...,q_n\}$, definimos $R_{ij}^k$ como el conjunto de las [[Conceptos Fundamentales#Cadena de Caracteres|Cadenas]] que parten del estado $i$ y terminan en el estado $j$ sin pasar por un estado mayor a $k$.

Definimos $R_{ij}^k$ de forma inductiva,
- Caso Base
$$\tag{1} R_{ij}^0=\{a \in \Sigma \mid \delta(q_i, a) = q_j \} : \text{ si } i \neq j$$
$$\tag{2} R_{ii}^0=\{a \in \Sigma \mid \delta(q_i, a) = q_i \} \cup \{ \varepsilon \} : \text{ si } i = j$$

- Caso Inductivo
$$\tag{3} R_{ij}^k=R_{ij}^{k-1} \cup R_{ik}^{k-1} \cdot (R_{kk}^{k-1})^\ast \cdot R_{kj}^{k-1}$$

Además, expresando $R_{ij}^k$ como una [[Expresiones Regulares|Expresión Regular]] obtenemos la siguiente expresión,
$$R_{ij}^k=R_{ij}^{k-1} | R_{ik}^{k-1} \cdot (R_{kk}^{k-1})^\ast \cdot R_{kj}^{k-1}$$

> [!info]  Observación
> Sea $Q$ el conjunto de estados con $|Q|=n$ y $F=\{f_1,...,f_m\}$ el conjunto de estados finales $\implies \bigcup_{j=1}^m R_{1 f_j}^n$ es el conjunto de cadenas aceptadas por el lenguaje. En otras palabras, es el lenguaje aceptado por el autómata.

> [!warning] Advertencia
> Este método esta pensado para ser implementado en un programa ya que el uso del mismo conlleva una gran cantidad de operaciones.