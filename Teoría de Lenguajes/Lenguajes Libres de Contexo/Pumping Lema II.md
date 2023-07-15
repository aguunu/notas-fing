Sea $L$ un [[Gramática Libre de Contexto#Lenguaje Libre de Contexto|LLC]], entonces, $\exists n \in \mathbb{N} : (\forall z)(z \in L \land |z| \geq n)$ de forma que $z$ se puede descomponer de la siguiente manera $z=uvwxy$ cumpliendo con las siguientes condiciones:

$$\tag{1} u v^i w x^i y \in L \; \forall i \geq 0$$

$$\tag{2} |vx| \gt 0$$

$$\tag{3} |vwx| \leq n$$

Es decir, siempre podemos hallar una cadena no vacía y no demasiado alejada del principio de $z$ que pueda “bombearse”; es decir, si se repiten $v$ y $x$ cualquier número de igual veces, o se borra (el caso en que $i = 0$), la cadena resultante también pertenece al lenguaje $L$.

***

Para probar que un lenguaje $L$ no es un [[Gramática Libre de Contexto#Lenguaje Libre de Contexto|LLC]] utilizando el *pumping lemma*, seguiremos los siguientes pasos:
1. Asumir por contradicción, que $L$ es un lenguaje regular con $n$ el largo del *pumping lemma* sobre $L$.
2. Construir un contra ejemplo con una [[Cadena de Caracteres|Cadena]] $z \in L$ con $|z| \geq n$.
3. Demostrar que para toda descomposición $z=uvwxy$ que cumplen con las condiciones $(2)$ y $(3)$ no cumplen con la condición $(1)$ ($\exists i \geq 1: u v^i w x^i y \notin L$).
