Dos o más [[Procesos]] están esperando indefinidamente por un evento que puede ser causado únicamente por alguno de estos procesos.

## Grafo de Asignación de Recursos
Es un *grafo de asignación de recursos* es un *grafo* cuyos vertices representan [[Procesos]] $(p_n)$ y recursos $(r_n)$. A su vez, sus aristas se definen de la siguiente manera,
- Existe una arista $p_i \rightarrow r_j$ si $p_i$ requiere el recurso $r_j$.
- Existe una arista $r_i \rightarrow p_j$ si el recurso $r_i$ esta asignado al proceso $p_j$.

Si el *grafo de asignación de recursos* no posee ciclos, entonces los procesos no sufrirán *deadlock*. Además, si existe una única instancia de cierto recurso, entonces, un ciclo implicaría *deadlock*. Sin embargo, si se tienen varias de estas instancias, un ciclo no implicaría necesariamente *deadlock*.

## Condiciones de Coffman
Las *condiciones de Coffman* son condiciones *necesarias* para la aparición de deadlocks.
1. **Exclusión Mutua**: Al menos un recurso debe ser de uso exclusivo, es decir, no compartible.
2. **Retención y Espera**: Un proceso debe mantener un recurso mientras espera para obtener otro.
3. **No Expropiable**: Los recursos se liberan voluntariamente.
4. **Espera Circular**: Un conjunto de procesos $\{p_0, p_1, ..., p_n\}$, $p_i$ esta esperando por $p_{i+1}$ y $p_n$ esta esperando por $p_0$.

## Abordar Deadlocks
En general, los sistemas operativos no se encargan de abordar el problema de *deadlock*. Por ende, el programador deberá seguir alguna de las siguientes estrategias:
- **Ignorar el Problema**.
- **Prevenir o Evitar**: Utilizar un protocolo para prevenir o evitar que ocurran deadlocks.
- **Detectar y Recuperarse**: Permitir que ocurran pero detectarlos y recuperarse.

### Algoritmo del Avestruz
Se espera que el *deadlock* no suceda, basándose en la baja probabilidad de este. Por lo tanto, se evita complejidad y aumenta el rendimiento en el sistema al no incluir detección o prevención de *deadlock*. Sin embargo, cuando se produce un *deadlock*, será necesario desactivar el sistema o eliminar un conjunto de procesos.

### Prevenir Deadlocks
Para *prevenir deadlocks* el sistema deberá asegurar que al menos una de las [[#Condiciones de Coffman]] no se cumpla.
1. Prevenir *"Exclusión Mutua"*
	- Hacer que los recursos sean "compartibles". *Sin embargo, no todos los recursos son "compartibles."*
2. Prevenir *"Retención y Espera"*
	- Garantizar que un proceso solo podrá solicitar un recurso cuando no tenga ningún recurso asignado. Los recursos serán asignados en conjuntos, es decir, el proceso solicita un conjunto de recursos y estos se asignarán al proceso si cada uno de ellos podrá ser asignado. Por lo tanto, un proceso deberá liberar todos sus recursos antes de solicitar nuevos recursos.
3. Prevenir *"No Expropiable"*
	- Si un proceso solicita un recurso que no se le podrá asignar inmediatamente, entonces, se liberarán todos los recursos que estén asignados a este proceso. Luego, el proceso continuara con su ejecución cuando pueda obtener los recursos que le fueron expropiados junto que el recurso que solicito.
4. Prevenir *"Espera Circular"*
	- Diseñar un protocolo para imponer un orden de los recursos y solicitarlos en dicho orden.

### Evitar Deadlocks
Para *evitar deadlocks* el sistema decide para cada solicitud si el proceso deberá esperar o no, en base a *información adicional*:
- Recursos disponibles.
- Recursos asignados a cada proceso.
- Futuras solicitudes de recursos.
- Liberaciones de cada proceso.

Se define el **estado de asignación de recursos** por la cantidad de recursos disponibles, los recursos asignados y las demandas máximas de los procesos.

#### Secuencia Segura
Una secuencia de procesos $p_0,...,p_n$ es segura para un estado $E$ si los recursos solicitados por cada proceso $p_i$ pueden ser satisfechos por los *recursos disponibles* + *recursos asignados* a todo $p_j : j<i$.

#### Estado Seguro
Un estado $E$ es *seguro* si existe una [[#Secuencia Segura]] para dicho estado. En otro caso, $E$ será un estado *inseguro* que podría conllevar a deadlock.

#### Algoritmos de Evitación
Un algoritmo de evitación asegura que el sistema siempre se encuentre en un [[#Estado Seguro]]. Estos algoritmos se clasifican según la cantidad de instancias por recurso.
- Única Instancia: Algoritmo de detección de ciclos en el [[#Grafo de Asignación de Recursos]], siendo un *estado seguro* si no se detectan ciclos y *estado inseguro* si se detectan ciclos.
- Múltiples Instancias: Algoritmo del Banquero.

>[!example] 
>Suponiendo que hay **3 recursos disponibles**, y el estado actual es el siguiente:
>
>||Máximo|En Uso|Podría Necesitar|
>|---|---|---|---|
>|$p_0$|$10$|$5$|$10-5=5$|
>|$p_1$|$4$|$2$|$4-2=2$|
>|$p_2$|$9$|$2$|$9-2=7$|
>
>Podemos observar que $p_1, p_0, p_2$ es una [[#Secuencia Segura]]. Pues
>- $p_1 \leftarrow 2 + 3 \geq 4$
>- $p_0 \leftarrow 5 + 2 + 3 \geq 10$
>- $p_2 \leftarrow 2 + 5 + 2 + 3 \geq 9$

##### Algoritmo del Banquero
Sea $n$ la cantidad de *procesos*, $m$ la cantidad de *recursos*. Entonces, declaramos las siguientes estructuras:
- `available[m]` un arreglo donde `available[j]` representa la cantidad de *unidades* disponibles para el recurso `j`.
- `allocation[n][m]` un arreglo bi-dimensional donde `allocation[i][j]` representa las *unidades* asignadas del recurso $j$ al proceso `i`.
- `max[n][m]` un arreglo bi-dimensional donde `max[i][j]` representa la cantidad máxima que podría estar asignada al proceso `i` sobre el recurso `j`.
- `need[n][m]` un arreglo bi-dimensional que representa la diferencia entre `max` y `allocation`, es decir, `need[i][j]` representa la cantidad que podría llegar a solicitar el proceso `i` sobre el recurso `j`.

1.
	`work[m]` un vector donde `work[i]` representa la cantidad de *unidades* disponibles para el recurso `i`.
	`finish[n]` un vector booleano inicializado en `False`.
2.
	Encontrar un `i` tal que `finish[i] = False` y `need[i] <= work`.
	Si no se encontró dicho `i`, Ir a $(3)$.
	`work[i] += allocation[i]`
	`finish[i] = True`
	Ir a $(2)$
3.
	Si `finish[i] = 1` para todo `i`, entonces, el sistema esta en [[#Estado Seguro]].

Sea $\{ p_1, ..., p_n\}, \{ r_1, ..., r_m \}$ los conjuntos de procesos y recursos respectivamente. Definimos las siguientes estructuras:
- $\vec{D}$ un vector de tamaño $m$, donde $D_j$ representa la cantidad disponible respecto a $r_j$.
- $\vec{A}$ una matriz de $n \times m$, donde $A_{ij}$ representa la cantidad de respecto a $r_j$ asignadas a $p_i$.
- $\vec{M}$ una matriz $n \times m$, donde $M_{ij}$ representa la cantidad máxima de recursos respecto a $r_j$ que podría llegar a ser usado por $p_i$.
- $\vec{N}$ una matriz $n \times m$ que representa la diferencia entre $\vec{M}$ y $\vec{A}$. En otras palabras, una matriz que representa la cantidad de recursos respecto a $r_j$ que podría llegar a ser solicitado por $p_i$.

1. $\vec{W}$ un vector de tamaño $m$ donde $W_i$ representa la cantidad de unidades disponibles para el recurso $i$.
2. $\vec{F}$ un vector de tamaño $n$ donde $F_i$ = `False` $, \forall i = 1,...,n$.
3. Mientras existe $i : F_i =$ `False` $\land$ $\vec{N_i} \leq \vec{W}$
	1. $W_i = W_i + A_i$
	2. $F_i =$ `True`
4. Si $F_i =$ `True` $\forall i = 1...n$, entonces, el sistema esta en [[#Estado Seguro]].

### Detectar y Recuperarse de Deadlocks
Para *detectar deadlocks* se emplea un algoritmo de detección para examinar el sistema y determinar si existe o no un deadlock.

Para recuperar el sistema luego de detectar un deadlock existen diferentes alternativas:
- Manual: Informar a un operario y realizar una recuperación manual.
- Automático: "Matar" procesos que estén involucrados en el deadlock. 

>[!bug] Matar Procesos
>Esta solución conlleva a nuevos problemas *(ej. datos corruptos si un proceso estaba modificando un archivo, perdida de computo del proceso).* Por ende, al momento de elegir a que procesos "matar" se deberá contemplar ciertos detalles del mismo y de esta forma minimizar el impacto en el sistema.
