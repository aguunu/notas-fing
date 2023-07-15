Decimos que un [[Lenguaje]] es *libre de contexto (LC) si existe alguna instancia de los siguientes objetos matemáticos que lo generen:
- [[Autómata Push-Down]]
- [[Gramática Libre de Contexto]]

## Propiedades de Clausura
Los [[Lenguaje Libre de Contexto]] son cerrados bajo las siguientes operaciones:

$$
\tag{Union}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ libre de contexto}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cup B}
$$

$$
\tag{Intersección}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ regular}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cap B}
$$

$$
\tag{Concatenación}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
B \textit{ libre de contexto}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{A \cdot B}
$$

$$
\tag{Clausura Kleene}
\underset{\textit{libre de contexto}}{A} \implies \underset{\textit{libre de contexto}}{A^\star}
$$

$$
\tag{Reverso}
\underset{\textit{libre de contexto}}{A} \implies \underset{\textit{libre de contexto}}{A^r}
$$

$$
\tag{Sustitución}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
f \textit{ sustitución}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{f(A)}
$$

$$
\tag{Homomorfismo}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
h \textit{ homomorfismo}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{h(A)}
$$

$$
\tag{Homomorfismo Inverso}
\left.
\begin{array}{l}
A \textit{ libre de contexto}\\
h \textit{ homomorfismo}
\end{array}
\right\}
\implies \underset{\textit{libre de contexto}}{h^{-1}(A)}
$$
