Una *expresión regular* es una cadena de caracteres que describe un [[Lenguaje Regular]]. 

Se define una expresión regular inductivamente de la siguiente manera:
- __CASO BASE__:
	1. $\emptyset$ es una *expresión regular* que define $\emptyset$
	2. $\varepsilon$ es una *expresión regular* que define $\{ \varepsilon \}$
	3. $a$ es una *expresión regular* que define $\{ a \}$
- __CASO INDUCTIVO__: Sean $r_1, r_2$ *expresiones regulares* tal que $\mathscr{L}(r_1) = L_1$ y $\mathscr{L}(r_2) = L_2$
	1. $(r_1 | r_2)$ es una *expresión regular* que define $L_1 \cup L_2$
	2. $(r_1 \cdot r_2)$ es una *expresión regular* que define $L_1 \cdot L_2$
	3. $(r_1^\ast)$ es una *expresión regular* que define $L_1^\ast$

>[!important] 
>Un [[Lenguaje]] $L$ es un [[Lenguaje Regular]] si existe una [[Expresiones Regulares|Expresión Regular]] $r$ tal que $\mathscr{L}(r)$ define a $L$.
