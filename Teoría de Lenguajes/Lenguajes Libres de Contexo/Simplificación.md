Sea $G=(V,T,P,S)$ una [[Gramática Libre de Contexto]], entonces, diremos que una *variable* $A \in V$ es,
- **Anulable** si $A \xRightarrow{\star} \varepsilon$
- **Positiva** si $A \xRightarrow{\star} x \in T^\star$
- **Alcanzable** si $S \xRightarrow{\star} \alpha A \beta$ con $\alpha, \beta \in (V \cup T)^\star$
- **Útil** si $S \xRightarrow{\star} \alpha A \beta \xRightarrow{\star} x \in T^\star$ con $\alpha, \beta \in (V \cup T)^\star$
Además, diremos que una *regla de producción* $p \in P$ es,
- **Unitaria** si es de la forma $A \rightarrow B$ con $A, B \in V$.
- $\varepsilon$***-producción***: si es de la forma $A \rightarrow \varepsilon$ con $A \in V$.

## Gramática Libre de Contexto Simplificada
Una [[Gramática Libre de Contexto]] esta *simplificada* cuando:
1. **NO** tiene *reglas de producción* de tipo $\varepsilon$*-producción*
2. __NO__ tiene *reglas de producción* de tipo *unitaria*.
3. __TODAS__ sus *variables* son de tipo *útil*.
4. __TODAS__ sus *variables* son de tipo *alcanzable*.

>[!success] Teorema
>Todo [[Lenguaje Libre de Contexto]] $L : L \neq \emptyset \land \varepsilon \notin L$ puede ser generado por una [[#Gramática Libre de Contexto Simplificada]].

>[!info] 
>Si el lenguaje $L=\emptyset$, entonces, $G=(\{S\}, \emptyset, \emptyset, S)$ es la mejor gramática que se puede generar para dicho lenguaje, siendo la variable $S$ *no útil*.
>
>Por otra parte, si $\varepsilon \in L$, entonces, la mejor gramática que se puede generar contendría la regla de producción $S \rightarrow \varepsilon$, la cual es una $\varepsilon$*-producción*.

***

## Algoritmo de Simplificación

FASE I (Reducción)
1. $G'=G$
2. $W_0 = \{ X \mid X \xRightarrow{\star} t \in T \}$
3. $i = 0$
4. DO
	1. $W_{i+1}= \{ X \mid X \in W_{i} \land X \xRightarrow{\star} t \in T \}$
	2. $i = i+1$
5. UNTIL ($W_i = W_{i+1}$)
6. FOR-EACH $A \rightarrow \alpha \in P$
	1. IF $(\exists X \in W_i \mid X \in \alpha)$
		1. Agregar($A \rightarrow \alpha$)
7. END

FASE II (Remover reglas de producción unitarias)
1. FOR-EACH $A \rightarrow B$
	1. FOR-EACH $B \rightarrow x : x \in T \lor x = \varepsilon$
		1. Agregar($A \rightarrow x$)
	2. END
	3. Remover($A \rightarrow B$)
4. END

FASE III (Remover $\varepsilon$*-producciones*)
1. FOR-EACH $A \rightarrow \varepsilon$
	1. FOR-EACH $X \rightarrow \alpha A \beta$
		1. Remover($X \rightarrow \alpha A \beta$)
		2. Agregar($X \rightarrow \alpha \beta$)
2. END
