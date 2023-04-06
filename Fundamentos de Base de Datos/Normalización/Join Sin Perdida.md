## Definición
Sea $D=\{R_1,...,R_m\}$ una descomposición de un esquema relacional $R$, decimos que $D$ cumple con **JSP** respecto al conjunto de *dfs* $F$ sobre $R$, si por cada instancia de relación $r$ de $R$ que satisfaga $F$ se cumple que $join(\prod_{R_1}(r),...,\prod_{R_m}(r)=r$

*Observación: **JSP** garantiza que no se generarán tuplas falsas al aplicar un join sobre las las relaciones de la descomposición.*

## Propiedades
Sea $D=\{R_1, R_2\}$ una descomposición sobre un esquema relacional $R$, decimos que $D$ tiene JSP respecto a $F$ sobre $R$ si y solamente si se cumple alguna de las siguientes condiciones.
1. La *df* $(R_1 \cap R_2) \rightarrow (R_1 - R_2)$ esta en $F^+$
2. La *df* $(R_1 \cap R_2) \rightarrow (R_2 - R_1)$ esta en $F^+$
*Observación: Si aplicamos la regla [[Dependencias Multivaluadas#^09a343 |RI7 Replica]] las siguientes propiedades también se cumplirán para dependencias multivaluadas.*

## Test de JSP
1. Crear una matriz $S$ con una fila $i$ por cada relación $R_i$ en la descomposición $D$, y una columna $j$ por cada atributo $a_j$ de $R$.
2. Hacer $S(i, j)=b_{ij}$ para todas las entradas de la matriz
3. Para cada fila $i$ que represente el esquema relacional $R_i$
	1. Para cada columna $j$ que represente el atributo $a_j$
		1. Si $R_i$ incluye a $a_j$ entonces hacer $S(i, j) = a_j$
4. Repetir hasta que una iteración no modifique $S$
	1. Para cada *df* $X \rightarrow Y$ en $F$
		1. Igualar los símbolos en los atributos de $Y$ para aquellas filas que coinciden en los atributos de $X$
5. Si una fila tiene todos los símbolos $a$, la descomposición cumple con **JSP**, en caso contrario, no cumple.





