## Alfabetos
Un alfabeto es un conjunto de símbolos finito y no vacío. Convencionalmente, utilizamos el símbolo $\Sigma$ para designar un alfabeto.
- $\Sigma = \{0,1\}$, el alfabeto binario.
- $\Sigma = \{a,b,...,z\}$, el conjunto de todas las letras minúsculas.

## Cadena de Caracteres
Una cadena de caracteres (palabra) es una secuencia finita de símbolos seleccionados de algún alfabeto.

Dado el alfabeto binario $\Sigma = \{0,1\}$,
  1. 01101 es una cadena de $\Sigma$
  2. 111 es una cadena de $\Sigma$

### Cadena Vacía $\varepsilon$
La cadena vacía es aquella cadena que presenta cero apariciones de símbolos. Esta cadena, designada por $\varepsilon$.
La cadena vacía se puede construirse en cualquier alfabeto.

### Longitud de una Cadena
Es el número de posiciones ocupadas por símbolos dentro de la cadena.
1. La cadena 01101 tiene una *longitud* de 5.
2. La cadena vacía $\varepsilon$ tiene una *longitud* de 0.
La notación estándar para indicar la longitud de una cadena $w$ es $|w|$.

Además, $|w|_a$ indica el número de posiciones ocupadas por el símbolo $a$ dentro de la cadena.

### Concatenación de Cadenas
Sean $x$ e $y$ dos cadenas. Entonces, $xy$ denota la concatenación de $x$ e $y$, es decir, la cadena formada por una copia de $x$ seguida de una copia de $y$.
1. Sean $x$ = 01101 e $y$ = 110. Entonces $xy$ = 01101110 e $yx$ = 11001101.

*Observación: para cualquier cadena $w$, se cumplen las ecuaciones $\varepsilon w = w \varepsilon = w$*

### Sufijo & Prefijo
Sea $w$ una cadena, entonces $x$ es *sufijo* de $w$ si existe $y$ tal que $w=yx$.
Análogamente se puede decir que $x'$ es prefijo de $w$ si existe $y'$ tal que $w=x'y'$.

### Potencias de un Alfabeto
Si $\Sigma$ es un alfabeto, podemos expresar el conjunto de todas las cadenas de una determinada longitud de dicho alfabeto utilizando una notación exponencial.
Definimos $\Sigma^k$ el conjunto de las cadenas de longitud $k$, tales que cada uno de los símbolos de las mismas pertenece a $\Sigma$.
*Observación: $\Sigma^0 = \{\varepsilon\}$ pues esta es la única palabra de largo igual a 0.*

#### Clausura de Kleene
El conjunto de todas las cadenas de un alfabeto $\Sigma$ se designa mediante $\Sigma^\ast$ *clausura de Kleene*.
1. $\{0,1\}^\ast = \{\varepsilon,0,1,00,01,10,11,000,...\}$.

*Observación: $\Sigma^\ast = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 ...$*

El conjunto de cadenas no vacías del alfabeto $\Sigma$ se designa como $\Sigma^+$. Por ende, 
- $\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 ...$
- $\Sigma^\ast = \Sigma^+ \cup \Sigma^0$
