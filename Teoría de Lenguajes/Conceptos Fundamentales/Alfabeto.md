Un *alfabeto* es un conjunto de *símbolos* finito y no vacío. Convencionalmente, utilizamos el símbolo $\Sigma$ para designar un alfabeto.
- $\Sigma = \{0,1\}$, el alfabeto binario.
- $\Sigma = \{a,b,...,z\}$, el conjunto de todas las letras minúsculas.

## Potencias de un Alfabeto
Definimos $\Sigma^k$ el conjunto de las cadenas de longitud $k$ sobre un alfabeto $\Sigma$.

>[!example] 
>1. $\{0,1\}^2 = \{00,01,10,11\}$
>2. $\{0, 1\}^0=\{\varepsilon\}$
>3. $\{a,b,c\}^1=\{a,b,c\}$
>4. $\Sigma$ un alfabeto arbitrario $\implies$ $\Sigma^0 = \{\varepsilon\}$

## Clausura de Kleene
La *clausura de Kleene* es el conjunto de todas las [[Cadena de Caracteres|Cadenas]] sobre un [[#Alfabetos|Alfabeto]] $\Sigma$ y se designa mediante $\Sigma^\star$.

El conjunto de *cadenas no vacías* sobre un [[#Alfabetos|Alfabeto]] $\Sigma$ se designa como $\Sigma^+$.

>[!example]
>1. $\{0,1\}^\ast = \{\varepsilon,0,1,00,01,10,11,000,...\}$
>2. $\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 ...$
>3. $\Sigma^\ast = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 ...$
>4. $\Sigma^\ast = \Sigma^+ \cup \Sigma^0$
