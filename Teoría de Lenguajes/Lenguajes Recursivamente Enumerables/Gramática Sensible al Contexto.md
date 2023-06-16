Una *gramática irrestricta* es un caso particular de [[Gramática Irrestricta]] donde todas sus reglas de producción son de la forma $$\alpha \rightarrow \beta$$

donde $\alpha, \beta \in (V \cup T)^\star \land \alpha \neq \varepsilon$ y además $\color{red} |\alpha| \leq |\beta|$.

*Esta última condición es la que lo diferencia con una [[Gramática Irrestricta]], representa que toda regla de producción es no-contractiva, es decir, al aplicar una regla, no se reduce el número de símbolos. Sin embargo, existe una excepción a esta y es la producción $S \rightarrow \varepsilon$, cuando el lenguaje contiene la tira vacía*.

## Lenguaje Sensible al Contexto
Un lenguaje $L$ es *sensible al contexto* si existe una [[Gramática Sensible al Contexto]] que lo genere.
