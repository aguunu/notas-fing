## Introducción
Una Dependencia Multivaluada $X \twoheadrightarrow Y$ se cumple cuando dos valores de atributos independientes Y, Z son determinados por un tercer atributo X.

## Dependencia Multivaluada Trivial
Una Dependencia Multivaluada $X \twoheadrightarrow Y$  es trivial en cualquiera de los siguientes casos.
1. $Y \subseteq X$
2. $X \cup Y = R$

*Observación: Si tenemos una DMV no trivial en una relación, tendremos valores redundantes en las tuplas.*

## Instancia valida de una DMV
Si existen dos tuplas $t_1$, $t_2$ en R tales que $t_1(X)$ = $t_2(X)$, entonces deberán existir también dos tuplas $t_3$, $t_4$ con las siguientes condiciones:
- $t_1(X) = t_2(X) = t_3(X) = t_4(X)$
- $t_1(Y)=t_3(Y)$  y  $t_2(Y)=t_4(Y)$
- $t_3(R-(XY))=t_2(R-(XY))$  y  $t_4(R-(XY))=t_1(R-(XY))$

### Ejemplo
Podemos observar que en la tabla se verifica la DMV $Name \twoheadrightarrow Course$ y a su vez $Name \twoheadrightarrow Hobby$

| Row | Name | Course | Hobby | 
|------|-------|---------|--------|
|$t_1$|Roberto|Calculo 1|Cantar|
|$t_2$|Roberto|Calculo 2|Dibujar|
|$t_3$|Roberto|Calculo 1|Dibujar|
|$t_4$|Roberto|Calculo 2|Cantar|

## Reglas de Inferencia
- `RI1 Reflexiva`  Si $Y \subseteq X$, entonces $X \rightarrow Y$
- `RI2 Aumento` $\{X \rightarrow Y\} \vDash XZ \rightarrow YZ$
- `RI3 Transitiva` $\{X \rightarrow Y, Y \rightarrow Z\} \vDash X \rightarrow Z$
- `RI4 Complemento` $\{X \twoheadrightarrow Y\} \vDash X \twoheadrightarrow (R - (X \cup Y))$
- `RI5 Aumento` Si $X \twoheadrightarrow Y$ y $Z \subseteq W$ entonces $WX \twoheadrightarrow YZ$
- `RI6 Transitiva` $\{X \twoheadrightarrow Y, Y \twoheadrightarrow Z\} \vDash X \twoheadrightarrow (Z - Y)$
- `RI7 Réplica` $\{X \rightarrow Y\} \vDash X \twoheadrightarrow Y$ ^09a343
- `RI8 Combinación` Si $X \twoheadrightarrow Y$ y existe $W$ tal que
	1. $W \cap Y = \emptyset$
	2. $W \rightarrow Z$
	3. $Z \subseteq Y$
	entonces $X \rightarrow Z$
	
## Dependencias Multivaluadas Embebidas
En un esquema de relación $R$ se cumple la dependencia multivaluada embebida $X \twoheadrightarrow Y \mid Z$ si para cualquier subesquema $R_i$ de $R$, tal que $R_i=X \cup Y \cup Z$ se cumple la dependencia $X \twoheadrightarrow Y$


