## Forma Normal de Chomsky
Decimos que una [[Gramática]] $G=(V,T,P,S)$ esta en *forma normal de Chomsky (FNC)* si sus reglas de producción $P$ son de la siguiente forma:

$$\tag{1} A \rightarrow BC$$

$$\tag{2} A \rightarrow a$$

donde $A, B, C \in V, a \in T$.

## Forma Normal de Greibach
Decimos que una [[Gramática]] $G=(V,T,P,S)$ esta en *forma normal de Greibach (FNG)* si sus reglas de producción $P$ son de la siguiente forma:

$$\tag{1} A \rightarrow a \beta$$

donde $a \in t, \beta \in V^\star$.

***

>[!success] Teorema
>Cualquier [[Gramática Libre de Contexto#Lenguaje Libre de Contexto|Lenguaje Libre de Contexto]] $L : \varepsilon \notin L$ puede ser generado con una [[Gramática Libre de Contexto#Gramática Libre de Contexto|Gramática Libre de Contexto]] en [[#Forma Normal de Greibach|FNG]] y también en [[#Forma Normal de Chomsky|FNC]].
