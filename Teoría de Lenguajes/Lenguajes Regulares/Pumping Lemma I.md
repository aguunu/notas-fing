Sea $L$ un [[Lenguaje Regular]], entonces, $\exists n \in \mathbb{N} : (\forall s \in L) (s \in L \land s |s| \geq n)$ de forma que $s$ se puede descomponer de la siguiente manera $s=xyz$ cumpliendo con las siguientes condiciones:

$$\tag{1} x y^i z \in L \; \forall i \geq 0$$

$$\tag{2} |y| \gt 0$$

$$\tag{3} |xy| \leq N$$

Es decir, siempre podemos hallar una cadena no vacía y no demasiado alejada del principio de $s$ que pueda “bombearse”; es decir, si se repite $y$ cualquier número de veces, o se borra (el caso en que $i = 0$), la cadena resultante también pertenece al lenguaje $L$.

***

Para probar que un lenguaje $L$ no es regular utilizando el *pumping lemma*, seguiremos los siguientes pasos:
1. Asumir por contradicción, que $L$ es un lenguaje regular con $N$ el largo del *pumping lemma* sobre $L$.
2. Construir un contra ejemplo con una [[Cadena de Caracteres|Cadena]] $s \in L$ con $|s| \geq N$.
3. Demostrar que para toda descomposición $s=xyz$ que cumplen con las condiciones $(2)$ y $(3)$ no cumplen con la condición $(1)$ (es decir existe un $i \geq 1: xy^iz \notin L$).

> [!example]
> Sea $L=\{x \mid x \text{ contiene una cantidad igual de 0s y 1s}\}$
> 
> 1. Supongamos que $L$ es un [[Lenguaje Regular]] con constante de *pumping lemma* igual a $N$.
> 2. Tomamos como contra ejemplo la cadena $s=0^N 1^N$, donde claramente $s \in L$ y además $|s| \geq N$. 
>    *Observar que al descomponer $s=xyz$ la condición $(3)$ fuerza a que $y$ este compuesta únicamente de $0s$.*
> 3. Luego, tomando $i=2$, obtenemos que $xy^2z \notin L$ pues $xy^2z$ posee más $0s$ que $1s$. Por ende, el lenguaje $L$ no es regular.
