Todos los lenguajes vistos en el curso corresponden a una clasificación denominada *jerarquía de Chomsky*.

$$\textit{Lenguajes de Tipo \textcolor{green}{$i+1$}} \subset \textit{Lenguajes de Tipo \textcolor{green}{$i$}}$$

|Tipo|Lenguaje|Autómata|Gramática|Ejemplo|
|:-:|:-:|:-:|:-:|:-:|
|0|[[Lenguaje Recursivamente Enumerable]]|[[Máquina de Turing]]|[[Gramática Irrestricta]]|$L = \{ w : w \textit{ describe una máquina de Turing}\}$|
|1|[[Lenguaje Sensible al Contexto]]|[[Autómata Lineal Acotado]]|[[Gramática Sensible al Contexto]]|$L = \{ a^n b^n c^n : n \geq 0\}$|
|2|[[Lenguaje Libre de Contexto]]|[[Autómata Push-Down]]|[[Gramática Libre de Contexto]]|$L=\{a^n b^n : n \geq 0\}$|
|3|[[Lenguaje Regular]]|[[Autómata Finito]]|[[Gramática Regular]]|$L=\{a^n : n \geq 0 \}$|

>[!important] 
>Sea $M$ un autómata de tipo $i$, entonces, $\mathscr{L}(M)$ es un [[Lenguaje]] de tipo $i$.

>[!important] 
>Sea $G$ una [[Gramática]] de tipo $i$, entonces, $\mathscr{L}(G)$ es un [[Lenguaje]] de tipo $i$.
