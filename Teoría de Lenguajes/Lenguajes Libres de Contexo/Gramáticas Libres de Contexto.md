Una *gramática libre de contexto* es una [[Gramática]] donde todas sus reglas de producción son de la forma $A \rightarrow \alpha$ donde $A \in V$ y $\alpha \in (V \cup T)^\star$.

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

## Gramática Ambigua
Una gramática es *ambigua* si existen dos o más [[#Árbol de Derivación|Árboles de Derivación]] para una cadena arbitraria.

>[!example] 
>Sea $G=(\{S\}, \{a+b,+,\star\}, \{S \rightarrow S+S \mid S \star S \mid a \mid b\}, S)$. Entonces, la cadena $a + a \star b$ puede ser generada de la siguientes formas:
>1. $S \rightarrow S+S \rightarrow a + S \rightarrow a + S \star S \rightarrow a + a \star S \rightarrow a + a \star b$
>2. $S \rightarrow S + S \star S \rightarrow a + S \star S \rightarrow a + a \star S \rightarrow a + a \star b$
>
>Por lo tanto, la gramática $G$ es ambigua.

## Lenguaje Generado

Dada una gramática $G=(V,T,P,S)$, el lenguaje generado por $G$ es $$L(G) = \{ x \in T^\star \mid S \xRightarrow{\star} x \}$$

En otras palabras, $L(G)$ es el conjunto de secuencias de $T^\star$ que se derivan del símbolo inicial $S$.

## Lenguaje Libre de Contexto
$L$ es un *lenguaje libre de contexto* si existe alguna [[#Gramática Libre de Contexto]] que lo genera.

>[!success] Teorema
>Todos los [[Lenguaje#Lenguaje Regular|Lenguajes Regulares]] son *libres de contexto*.

### Propiedades de Clausura

$$
\tag{Union}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ libre de contexto}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cup B}
$$

$$
\tag{Intersección}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ regular}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cap B}
$$

$$
\tag{Concatenación}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ libre de contexto}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cdot B}
$$

$$
\tag{Clausura Kleene}
\underset{\textit{libre de contexto}}{A} \implies \underset{\textit{libre de contexto}}{A^\star}
$$

$$
\tag{Reverso}
\underset{\textit{libre de contexto}}{A} \implies \underset{\textit{libre de contexto}}{A^r}
$$

$$
\tag{Sustitución}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
f \textit{ sustitución}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{f(A)}
$$

$$
\tag{Homomorfismo}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
h \textit{ homomorfismo}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{h(A)}
$$

$$
\tag{Homomorfismo Inverso}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
h \textit{ homomorfismo}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{h^{-1}(A)}
$$

## Gramática Regular
Una *gramática regular* es una [[#Gramática Libre de Contexto]] en la que __todas__ sus *reglas de producción* son o bien *gramática lineal izquierda* o *gramática lineal derecha*,
- **Gramática Lineal Izquierda**: $A \rightarrow Bw \mid w$
- **Gramática Lineal Derecha**: $A \rightarrow wB \mid w$
donde $A, B \in V$ y $w \in (T \cup \{\varepsilon\})$.

>[!warning] 
>Mezclar reglas de *gramática lineal izquierda* y *gramática lineal derecha* no implica que el lenguaje sea regular.
>
>Podemos observar que $G=(\{S, A\}, \{0, 1\}, P, S)$ con $P = \{ S \rightarrow A \cdot 0 , A \rightarrow 1 \mid 1 \cdot S \}$ genera el lenguaje $\{ 0^k \cdot 1^k : k > 0 \}$ el cual no es regular.
>

### Gramática Extendida 
Una *gramática regular* es una *gramática extendida* cuando $w \in T^\star$.
