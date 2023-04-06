## Dependencia Funcional
Una *dependencia funcional* $X \rightarrow Y$, entre dos conjuntos de atributos $X$ e $Y$ que a su vez son subconjuntos de un esquema relacional $R$, especifica una restricción sobre las posibles tuplas que formarían una instancia $r$ de $R$.
Para cualquier par de tuplas $t_1, t_2$ de $r$ tal que $t_1(X)=t_2(X)$, entonces debemos tener que $t_1(Y)=t_2(Y)$

*Observación: Si $X$ es una clave candidata de $R$, entonces $X \rightarrow Y$ para cualquier subconjunto $Y$ de $R$.*

## Clausura
### Clausura de un Conjunto de *dfs*
Sea $F$ un conjunto de *dfs (dependencias funcionales)* entonces denotamos $F^+$ como el conjunto de todas las *dfs* que se cumplen en todas las instancias que satisfacen $F$.

### Clausura de un Conjunto de Atributos
Sea $X$ un conjunto de atributos de un esquema relacional $R$, y $F$ un conjunto de dependencias funcionales sobre $R$, definimos $X^+$ como el conjunto de los atributos determinados funcionalmente por $X$.

## Reglas de Armstrong
Son reglas minimales con las que se pueden derivar las demás.
- `RI1 Reflexiva` Si $Y \subseteq X$, entonces $X \rightarrow Y$
- `RI2 Aumento` $\{X \rightarrow Y\} \vDash XZ \rightarrow YZ$
- `RI3 Transitiva` $\{X \rightarrow Y, Y \rightarrow Z\} \vDash X \rightarrow Z$

## Equivalencia de Conjuntos
Dos conjuntos $F_1, F_2$ de *dfs* son equivalentes entre si y solamente si $F_1^+=F_2^+$ 

*Observación: Las dfs de $F_1$ se pueden inferir de $F_2$ y viceversa.*
*Observación: $F_1$ cubre $F_2$ y viceversa.*

### Determinar si $F_1$ cubre a $F_2$
1. Para cada *df* $X \rightarrow Y$ de $F_1$, calcular $X^+(F_1)$ y verificar que $X^+$ incluya los atributos en $Y$.