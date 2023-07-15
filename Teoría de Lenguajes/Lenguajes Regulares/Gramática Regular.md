Una *gramática regular* es una [[Gramática]] en la que __TODAS__ sus *reglas de producción* son o bien *lineales izquierda* o *lineales derecha*, de esta forma, definiendo un [[Lenguaje Regular]].
- **Lineal Izquierda**: $A \rightarrow Bw \mid w$
- **Lineal Derecha**: $A \rightarrow wB \mid w$
donde $A, B \in V$ y $w \in T^\star$.

Una [[Gramática Regular]] es una __Gramática Lineal Izquierda__ si __TODAS__ sus *reglas de producción* son *lineales izquierda*, o es una __Gramática Lineal Derecha__ en el caso en que __TODAS__ todas sus *reglas de producción* son *lineales derecha*.

>[!warning] 
>Mezclar reglas de *gramática lineal izquierda* y *gramática lineal derecha* no implica la definición de un [[Lenguaje Regular]].
>
>Podemos observar que $G=(\{S, A\}, \{0, 1\}, P, S)$ con $P = \{ S \rightarrow A \cdot 0 , A \rightarrow 1 \mid 1 \cdot S \}$ genera el lenguaje $\{ 0^k \cdot 1^k : k > 0 \}$ el cual no es regular.
