El *pumping lemma* se utiliza para probar que un [[Lenguaje]] no es [[Lenguaje#Lenguaje Regular|Regular]].

Si $L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]], entonces $L$ tiene un largo *pumping* $N$, de forma que cualquier [[Conceptos Fundamentales#Cadena de Caracteres|Cadena]] $s$ donde $|s| \geq N$ podrá ser expresadas de la siguiente manera $s=xyz$ (pumped) cumpliendo con las siguientes condiciones:
$$\tag{1} x y^i z \in L \; \forall i \geq 0$$
$$\tag{2} |y| \gt 0$$
$$\tag{3} |xy| \leq N$$
Para probar que un lenguaje $L$ no es regular utilizando el *pumping lemma*, seguiremos los siguientes pasos:
1. Asumir que $L$ es un lenguaje regular.
2. $L$ debe tener un largo *pumping* ($N$).
3. Todas las cadenas de largo mayor a $N$ pueden ser *pumped*.
4. Encontrar una cadena $s$ en $L$ tal que $|s| \geq N$.
5. Expresar $s$ como $xyz$.
6. Demostrar que $xy^iz \notin L$ para algún $i$.
7. Considerar todas las maneras en las que $s$ puede ser expresada como $xyz$.
8. Demostrar que ninguna de estas satisface las 3 condiciones del *pumping lemma*.
9. $s$ no puede ser *pumped*. (Contradicción).

