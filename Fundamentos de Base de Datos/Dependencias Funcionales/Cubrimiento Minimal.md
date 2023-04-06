## Conjunto Minimal
Sea $F$ un conjunto de *dfs*, decimos que $F$ es minimal si y solamente si:
- Toda *df* de $F$ tiene un solo atributo a la derecha.
- No podemos remplazar ninguna *df* $X \rightarrow a$ de $F$ por una *df* $Y \rightarrow a$, donde $Y \subset X$ y seguir teniendo un conjunto equivalente a $F$.
- No podemos eliminar ninguna *df* de $F$ y seguir teniendo un conjunto de *dfs* equivalente a $F$.

Un **Cubrimiento Minimal** de $F$ es un conjunto minimal $F_{min}$ equivalente a $F$.

## Algoritmo
1. Hacer $G = F$
2. Remplazar cada *df* $X \rightarrow a_1,...,a_n$ en $G$ por las *dfs* $X \rightarrow a_1,..., X \rightarrow a_2$ *(descompone la parte derecha de las dfs)*
3. Para cada *df* $X \rightarrow a$ en $G$
	1. Para cada atributo $b$ que sea un elemento de $X$
		1. Calcular $(X-b)^+$ respecto a $G$, si $(X-b)^+$ contiene el atributo $a$, reemplazar $X \rightarrow a$ por $(X-b) \rightarrow a$ en $G$
	*(elimina atributos redundantes del lado izquierdo)*
4. Para cada *df* $X \rightarrow a$ en $G$
	1. Calcular $X^+$ respecto a $(G-(X \rightarrow a))$, si $X^+$ contiene el atributo $a$, eliminar $X \rightarrow a$ de $G$.
	*(elimina dfs redundantes)*
