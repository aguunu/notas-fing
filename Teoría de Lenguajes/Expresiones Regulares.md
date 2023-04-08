Una expresión regular es una cadena de caracteres que describe un *lenguaje regular*.

Se puede definir inductivamente de la siguiente forma:
- **Paso Base**
	1. $\emptyset$ es una *expresión regular* que define $\emptyset$
	2. $\varepsilon$ es una *expresión regular* que define $\{ \varepsilon \}$
	3. $a$ es una *expresión regular* que define $\{ a \}$

Sea $r_1$ una *expresión regular* que define el [[Lenguaje]] $L_1$.
Sea $r_2$ una *expresión regular* que define el [[Lenguaje]] $L_2$. 
- **Paso Inductivo**
	1. $(r_1 | r_2)$ es una *expresión regular* que define $L_1 \cup L_2$
	2. $(r_1 \cdot r_2)$ es una *expresión regular* que define $L_1 \cdot L_2$
	3. $(r_1^*)$ es una *expresión regular* que define $L_1^*$