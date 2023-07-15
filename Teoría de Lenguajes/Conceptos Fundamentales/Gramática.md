Definimos una *gramática* $G$ como $G=(V,T,P,S)$ donde,
- $V$ el conjunto de variables.
- $T$ el conjunto de símbolos terminales.
- $P$ el conjunto de reglas de producción.
- $S \in V$ el símbolo inicial.

## Derivación
Una *derivación* representa la inferencia de una regla de producción. Dada una [[Gramática]] $G=(V,T,P,S)$, escribimos $\alpha A \beta \implies \alpha \gamma \beta$ cuando queremos mostrar que $\gamma$ es el resultado de aplicar la regla $A \implies \gamma$ con $A \in V$ y $\alpha, \beta, \gamma \in (V \cup T)^\star$.

Para indicar que la inferencia se produce en $n$ pasos, $\alpha A \beta \xRightarrow{n} \alpha \gamma \beta$. En caso de querer representar una cantidad indefinida de pasos se utiliza $\star$ en vez de $n$.

### Derivación de más a la Izquierda
Una *derivación de más a la izquierda* es una secuencia de derivaciones en la que cada paso se deriva sobre la variable que este más a la izquierda.

### Derivación de más a la Derecha
Definición análoga a [[#Derivación de más a la Izquierda]].

## Árbol de Derivación
Un *árbol de derivación* es un árbol ordenado que gráficamente representa la información semántica de cadenas derivadas de una [[#Gramática Libre de Contexto]].

>[!success] Teorema 
>Dada una gramática $G=(V,T,P,S)$ y una cadena $w \in T^\star$
>
>$$S \xRightarrow{\star} w \iff \exists \text{ un árbol de derivación para } w$$

## Lenguaje Generado

Dada una gramática $G=(V,T,P,S)$, el lenguaje generado por $G$ es $$\mathscr{L}(G) = \{ x \in T^\star \mid S \xRightarrow{\star} x \}$$

En otras palabras, $\mathscr{L}(G)$ es el conjunto de secuencias de $T^\star$ que se derivan del símbolo inicial $S$.

## Gramática Ambigua
Una gramática es *ambigua* si existen dos o más [[#Árbol de Derivación|Árboles de Derivación]] para una cadena arbitraria.

>[!example] 
>Sea $G=(\{S\}, \{a+b,+,\star\}, \{S \rightarrow S+S \mid S \star S \mid a \mid b\}, S)$. Entonces, la cadena $a + a \star b$ puede ser generada de la siguientes formas:
>1. $S \rightarrow S+S \rightarrow a + S \rightarrow a + S \star S \rightarrow a + a \star S \rightarrow a + a \star b$
>2. $S \rightarrow S + S \star S \rightarrow a + S \star S \rightarrow a + a \star S \rightarrow a + a \star b$
>
>Por lo tanto, la gramática $G$ es ambigua.
