Una *cadena de caracteres* es una secuencia finita de símbolos seleccionados de algún [[Alfabeto]].

>[!example] 
>Sea $\Sigma$ un alfabeto tal que $\Sigma = \{0,1\}$,
>  1. $01101$ es una cadena de $\Sigma$
>  2. $111$ es una cadena de $\Sigma$
>  3. $01121$ **NO** es una cadena de $\Sigma$

## Cadena Vacía $\varepsilon$
La *cadena vacía* $\varepsilon$ es aquella [[#Cadena]] que presenta cero apariciones de símbolos.

>[!info] 
> La cadena vacía puede construirse en cualquier alfabeto.

## Longitud de una Cadena
La *longitud de una cadena* $w$ es el número de posiciones ocupadas por símbolos dentro de $w$, y se denota $|w|$. Además, el número de posiciones ocupadas por un símbolo $a$ dentro de $w$ se denota $|w|_a$.

>[!example] 
>1. $|aabab|=5$
>2. $|\varepsilon|=0$
>3. $|aaba|_a=3$

## Concatenación de Cadenas
Sean $x$ e $y$ dos cadenas. Entonces, $xy$ denota la concatenación de $x$ e $y$, es decir, la cadena formada por una copia de $x$ seguida de una copia de $y$.

Cualquier cadena $w$, cumple con las siguientes ecuaciones: 

$$\varepsilon w = w \varepsilon = w$$

> [!example]
>  Sean $x = 01101, y = 110$,
>  1. $xy = 01101110$
>  2. $yx = 11001101$

## Sufijo & Prefijo
Sea $w$ una cadena, entonces $x$ es *sufijo* de $w$ si existe $y$ tal que $w=yx$.
Análogamente se puede decir que $x'$ es prefijo de $w$ si existe $y'$ tal que $w=x'y'$.
