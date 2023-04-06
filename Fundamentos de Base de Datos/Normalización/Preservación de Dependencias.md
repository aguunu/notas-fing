## Proyección de Dependencias
Dado un conjunto de *dfs* $F$ sobre un esquema de relación $R$, y $R_i$ un subconjunto de $R$, la proyección de $F$ sobre $R_i$ se denota $\prod_{R_i}(F)$ y es el conjunto de *dfs* $X \rightarrow Y$  en $F^+$ tal que todos los atributos de $X \cup Y$ están contenidos en $R_i$

## Preservación de Dependencias
Sea $D=\{R_1,...,R_m\}$ una descomposición de un esquema relacional $R$, decimos que $D$ preserva las dependencias respecto a $F$ si se cumple: $(\bigcup(\prod_{R_i(F)}))^+ = F^+$