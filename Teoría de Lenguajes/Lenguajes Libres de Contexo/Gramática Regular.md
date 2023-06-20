Una *gramática regular* es una [[Gramática Libre de Contexto]] en la que __todas__ sus *reglas de producción* son o bien *gramática lineal izquierda* o *gramática lineal derecha*,
- **Gramática Lineal Izquierda**: $A \rightarrow Bw \mid w$
- **Gramática Lineal Derecha**: $A \rightarrow wB \mid w$
donde $A, B \in V$ y $w \in (T \cup \{\varepsilon\})$.

De esta forma, generando un [[Expresiones Regulares|Lenguaje Regular]].

>[!warning] 
>Mezclar reglas de *gramática lineal izquierda* y *gramática lineal derecha* no implica la definición de un [[Expresiones Regulares|Lenguaje Regular]].
>
>Podemos observar que $G=(\{S, A\}, \{0, 1\}, P, S)$ con $P = \{ S \rightarrow A \cdot 0 , A \rightarrow 1 \mid 1 \cdot S \}$ genera el lenguaje $\{ 0^k \cdot 1^k : k > 0 \}$ el cual no es regular.
>

## Gramática Extendida 
Una *gramática regular* es una *gramática extendida* cuando $w \in T^\star$.
