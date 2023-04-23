Una *expresión regular* es una cadena de caracteres que describe un *lenguaje regular*. Se define una expresión regular inductivamente de la siguiente manera:

- Caso Base,
	1. $\emptyset$ es una *expresión regular* que define $\emptyset$
	2. $\varepsilon$ es una *expresión regular* que define $\{ \varepsilon \}$
	3. $a$ es una *expresión regular* que define $\{ a \}$
	
- Caso Inductivo,
	Sean $r_1, r_2$ *expresiones regulares* de forma que $L(r_1) = L_1$ y $L(r_2) = L_2$
	1. $(r_1 | r_2)$ es una *expresión regular* que define $L_1 \cup L_2$
	2. $(r_1 \cdot r_2)$ es una *expresión regular* que define $L_1 \cdot L_2$
	3. $(r_1^\ast)$ es una *expresión regular* que define $L_1^\ast$
