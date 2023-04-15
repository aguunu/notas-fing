El *pumping lemma* se utiliza para probar que un [[Lenguaje]] no es [[Lenguaje#Lenguaje Regular|Regular]].

Si $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]], entonces $L$ tiene un largo *pumping* $N$, de forma que cualquier [[Conceptos Fundamentales#Cadena de Caracteres|Cadena]] $s$ donde $|s| \geq N$ podrá ser expresadas de la siguiente manera $s=xyz$ cumpliendo con las siguientes condiciones:
$$\tag{1} x y^i z \in L \; \forall i \geq 0$$
$$\tag{2} |y| \gt 0$$
$$\tag{3} |xy| \leq N$$
Para probar que un lenguaje $L$ no es regular utilizando el *pumping lemma*, seguiremos los siguientes pasos:
1. Asumir por contradicción, que $L$ es un lenguaje regular. Sea $N$ el largo del *pumping lemma*.
2. Construir un contra ejemplo con una [[Conceptos Fundamentales#Cadena de Caracteres|Cadena]] $s \in L$ con $|s| \geq N$.
3. Demostrar que para toda descomposición $s=xyz$ que cumplen con las condiciones $(2)$ y $(3)$ no cumplen con la condición $(1)$ (es decir existe un $i \geq 1: xy^iz \notin L$).

> [!example] 
> Sea $L=\{x: x \text{ contiene una cantidad igual de 0s y 1s}\}$
> 
> 1. Supongamos que $L$ es [[Lenguaje#Lenguaje Regular|Regular]] con largo de *pumping lemma* $N$.
> 2. Tomamos como contra ejemplo la cadena $s=0^N 1^N$, donde claramente $s \in L$ y además $|s| \geq N$. 
>    *Observar que al descomponer $s=xyz$ la condición $(3)$ fuerza a que $y$ este compuesta únicamente de $0s$.*
> 3. Luego, tomando $i=2$, obtenemos que $xy^2z \notin L$ pues $xy^2z$ tiene más $0s$ que $1s$.



