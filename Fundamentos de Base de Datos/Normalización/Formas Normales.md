## 1NF
Un Esquema Relacional $R$ está en 1NF si los dominios de los atributos incluyen solo valores atómico (los atributos no pueden ser multivaluados ni compuestos).
*Observación: Cualquier diseño relacional esta en 1FN.*

## 2NF
Un Esquema Relacional $R$ está en 2NF si ningún *atributo no primo* $a$ de $R$ *depende parcialmente* de cualquier *clave* de $R$

## 3NF
Un Esquema Relacional $R$ está en 3NF si está en 2NF y ningún *atributo no primo* de $R$ depende transitivamente de una *clave* de $R$.

Un Esquema Relacional $R$ está en 3NF, si siempre que una *df* $X \rightarrow a$ se cumple en $R$ se cumple alguna de las siguientes condiciones:
- $X$ es una *superclave* de $R$
- $a$ es un *atributo primo* de $R$

### Descomposición en 3NF con Preservación de Dependencias
1. Encontrar un cubrimiento minimal $G$ para $F$
2. Para cada miembro izquierdo $X$ de una *df* que aparezca en $G$
	1. Crear un esquema relacional $\{X \cup a_1 ... \cup a_m\}$ en $D$, donde $X \rightarrow a_1, ..., X \rightarrow a_m$ sean las únicas *dfs* en $G$ con $X$ como miembro izquierdo.
3. Colocar todos los atributos restantes (aquellos que no fueron colocados en ningún esquema relacional) en un solo esquema relacional.
*Observación: El paso 3 es para asegurar la propiedad de preservación de dependencias.*

### Descomposición en 3NF con JSP y Preservación de Dependencias
1. Aplicar el algoritmo de *Descomposición en 3NF con Preservación de Dependencias.*
2. Eliminar esquemas relacionales redundantes (aquellos que estén contenidos en otro esquema relacional).

## BCNF
Un Esquema Relacional $R$ está en BCNF, si siempre que una *df* $X \rightarrow a$ se cumple en $R$, entonces $X$ es una *superclave* de $R$

### Descomposición BCNF con JSP
1. Hacer $D$ = $R$
2. Mientras haya un ER $Q$ en $D$ que no esté en BCNF:
	1. Escoger un ER $Q$ en $D$ que no esté en BCNF
	2. Encontrar una *df* $X \rightarrow Y$ que viole BCNF
	3. Reemplazar $Q$ en $D$ por dos esquemas $(Q-Y)$ y $(X \cup Y)$

## 4NF
### Definición
Un Esquema Relacional $R$ esta en 4FN respecto a un conjunto de dependencias $F$ si para cualquier *dmv* no trivial $X \twoheadrightarrow Y$ en $F^+$, $X$ es superclave de $R$

### Descomposición en 4NF con JSP
1. Hacer $D$ = $R$
2. Mientras haya un ER $Q$ en $D$ que no esté en 4NF:
	1. Escoger un ER $Q$ en $D$ que no esté en 4NF
	2. Encontrar una *dmv* $X \twoheadrightarrow Y$ que viole 4NF
	3. Reemplazar $Q$ en $D$ por dos esquemas $(Q-Y)$ y $(X \cup Y)$

*Observación: el algoritmo es similar a BCNF*

### Propiedades JSP en 4NF
Sea $D=\{R_1, R_2\}$ una descomposición de un esquema relacional $R$, decimos que $D$ cumple con **JSP** respecto a $F$ sobre $R$ si y solamente si se cumple alguna de las siguientes condiciones.
1. La *dmv* $(R_1 \cap R_2) \twoheadrightarrow (R_1 - R_2)$ esta en $F^+$
2. La *dmv* $(R_1 \cap R_2) \twoheadrightarrow (R_2 - R_1)$ esta en $F^+$

*Observación: Esta propiedad sirve tanto para las dmvs como las dfs (dado que una df también es una dmv)*

### Ejemplos
Sea $R$
| Name | Course | Hobby | 
|-------|---------|--------|
|Roberto|Calculo 1|Cantar|
|Roberto|Calculo 2|Dibujar|
|Roberto|Calculo 1|Dibujar|
|Roberto|Calculo 2|Cantar|

Podemos observar que $R$ no se encuentra en 4NF pues:
- $Name \twoheadrightarrow Course$
- $Name \twoheadrightarrow Hobby$
- $Name$ no es superclave

Sea $R=\{R_1, R_2\}$
donde $R_1$
| Name | Course |
|-------|---------|
|Roberto|Calculo 1|
|Roberto|Calculo 2|
|Roberto|Calculo 1|
|Roberto|Calculo 2|

y $R_2$
| Name | Hobby |
|-------|---------|
|Roberto|Cantar|
|Roberto|Dibujar|
|Roberto|Dibujar|
|Roberto|Cantar|
- $Name \twoheadrightarrow Course$, trivial pues $Name \cup Course = R_1$
- $Name \twoheadrightarrow Hobby$, trivial pues $Name \cup Hobby = R_2$
Por lo tanto, $R_1$ y $R_2$ están en 4NF, entonces $R$ está en 4NF.
