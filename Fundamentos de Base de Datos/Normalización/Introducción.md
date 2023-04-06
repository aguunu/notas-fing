## Superclave
Una superclave de $R=\{a_1,...,a_n\}$ es un conjunto de atributos $S \subseteq R$ tal que no existen dos tuplas $t_1, t_2$ distintas en ningún $r$ tal que $t_1(S) = t_2(S)$

## Clave
Una clave $K$ es una superclave que cumple que si se le quita alguno de sus atributos deja de ser superclave.
*Observación:*
*Sea $a$ un atributo de un esquema relacional $R$, dicho atributo,*
- *Esta en toda clave: nunca aparece a la derecha de alguna df de $R$.*
- *No esta en ninguna clave: solo aparece a la derecha de las df de $R$.*
- *En otro caso, puede o no estar en alguna clave.*

## Clave Candidata | Clave Primaria
Si una relación tiene más de una clave, cada una es una clave candidate. Una de ellas es arbitrariamente designada como clave primaria. El resto serán claves secundarias.

## Atributo Primo
Un atributo de un esquema de relación $R$ es primo si es miembro de alguna clave de $R$

*Observación: Un atributo es no primo si no pertenece a ninguna clave de $R$*

## Dependencia Total
$X \rightarrow Y$ es una *df* total si la eliminación de cualquier atributo $a$ de $X$ hace que la *df* deje de ser válida.

*Observación: Una dependencia total es aquella que no tiene atributos redundantes a la izquierda.*

## Dependencia Parcial
$X \rightarrow Y$  es una *df* parcial si es posible eliminar un atributo $a$ de $X$ y la *df* sigue siendo válida.

## Dependencia Transitiva
$X \rightarrow Y$ es una *df* transitiva en un esquema relacional $R$ si existe un conjunto de atributos $Z$ que no sea un subconjunto de una clave de $R$ y se cumple tanto $X \rightarrow Z$ y $Z \rightarrow Y$
