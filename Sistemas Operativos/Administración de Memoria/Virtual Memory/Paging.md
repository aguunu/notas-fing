La idea de *paging* es dividir la memoria en *frames* de un tamaño fijo $k$, donde luego, serán colocadas *pages* del mismo tamaño que los frames, es decir, de tamaño $k$. Y de esta forma,  asignarle a un proceso un conjunto de *pages* para que luego el SO mantenga en los *frames* aquellas partes del proceso que están siendo usadas.

>[!success] Fragmentación Externa
>Al dividir la memoria en *frames* de tamaño fijo, se elimina la [[Fragmentación#Fragmentación Externa|Fragmentación Externa]]. Sin embargo, esta técnica no elimina la [[Fragmentación#Fragmentación Interna|Fragmentación Interna]].

Cada *page* posee un *page number*. Por ende, una [[Virtual Memory#Virtual Address|Virtual Address]] se descompone de la siguiente manera:
- Los $m-n$ bits de mayor orden representan el *page number*.
- Los restantes $n$ bits representan el *page offset*.

## Page Fault
Un *page fault* se genera cuando un proceso intenta acceder a una pagina que no esta cargada en memoria principal.

Para atacar este problema, surgen diferentes estrategias sobre demanda de paginas.
- Demanda Pura: La pagina se carga en memoria principal únicamente cuando es solicitada.
- Paginación Previa: Además de cargar en memoria principal la pagina solicitada, también se cargarán otras paginas adicionales.

Sea $p$ la probabilidad de un *page fault* al demandar una pagina, el *effective access time (EAT)* se calcula de la siguiente forma:
$$EAT=(1-p) \cdot M + p \cdot T$$
donde $M$ es el tiempo de acceso a memoria y $T$ es el tiempo para resolver un *page fault*.

El tiempo $T$ para resolver un *page fault* incluye las siguientes tareas:
1. Generar una interrupción por el sistema operativo.
2. Determinar si se debe a un *page fault*.
3. Guardar el estado del proceso.
4. Ejecutar el *Scheduler* ($\star$) (para aprovechar el CPU mientras se espera).
5. Solicitar la lectura de la pagina a memoria secundaria.
6. Esperar la transferencia de la memoria secundaria.
7. Atender la rutina de completitud de la operación de IO de la memoria secundaria.
8. Guardar el estado del proceso en ejecución ($\star$).
9. Actualizar la [[#Page Table]]
10. Esperar a que se asigne el CPU sea nuevamente asignado al CPU.
11. Restaurar el estado y continuar con la ejecución del proceso.

## Page Table
Estructura de datos que se almacena en memoria principal y se encarga de mapear una [[Virtual Memory#Virtual Address|Virtual Address]] a una *physical address*. Esta es accedida por el [[Memory Management Unity|MMU]] a través del registro *page table base register (PTBR)*. 

>[!success] Compartir Paginas
>Los procesos que comparten datos entre ellos, podrán compartir de forma eficiente *pages* entre ellos. Pues en la *page table* de estos proceso, tendrán referenciado el *frame* que contiene dicha *page*.

>[!example] 
>Una memoria de $256$ bytes que direcciona de a $4$ bytes. Y a su vez, *pages* de $16$ bytes, entonces:
>
>- Para referenciar los $256$ bytes de memoria de a $4$ bytes, necesitamos $6$ bits. Pues $2^6=256 / 4$.
>- La *page table* tendrá $256 / 16 = 16$ entradas. Por ende, para el *page number* necesitamos $4$ bits, pues $2^4=16$. Luego, los bits restantes serán utilizados para el *page offset*, es decir, $6-4=2$ bits.
>  
>  Dada la *virtual address* $\overset{6 \textendash bits}{\overbrace{ \overset{page}{\overbrace{0011}} \overset{offset}{\overbrace{01}}}}$, el *page number* ($4$ bits) es $0011=3$ con *offset* ($2$ bits) $01=1$.
>  
>  Luego, para hallar su respectivo *frame* basta con buscar a que *frame* esta asociado dicho *page number* en la *page table*.
>  
>  Una vez obtenido el *frame*, hallamos la *physical address* agregando el *offset* hallado anteriormente.

### Forward-Mapped
Consiste en dividir la *page table* formando una jerarquía por niveles. Los bits $b_m b_{m-1} ... b_0$ correspondiente al *page number* en la *virtual address* se divide en $n$ segmentos de bits $s_0 s_1 ... s_{n-1}$ donde cada uno de ellos identifica un nivel en la jerarquía.

Luego, se toma la tabla correspondiente al primer nivel y se identifica el próximo nivel usando los bits del segmento correspondiente a este nivel, este procedimiento se repite hasta llegar al último nivel. En el último nivel, se identificará (usando el segmento correspondiente) el *frame* asociado a la *virtual address*.

### Inverted
Se utiliza una única *page table* en común para todos los procesos. De esta forma, reduciendo el espacio de almacenamiento y aumentando el tiempo de búsqueda.

### Hash-Map
Se usa un *hash-map* (con *listas* para colisiones), mapeando un *page number* a su correspondiente *frame*.

## Translation Look-Aside Buffer
El *translation look-aside buffer (TLB)* es una memoria de rápido acceso asociativa, que funciona como una memoria caché para la [[#Page Table]]. Además, por cada asociación se agrega un *dirty bit* para verificar que el dato sea correcto.

>[!success] 
>El funcionamiento del TLB es similar al de una memoria caché, es decir, si no encuentra el dato, hará un *miss* y procede a usar la *page table*, luego se cargará en el TLB el dato. En otro caso, se realizará un *hit* y no será necesario usar la *page table*.

Costo de un acceso efectivo a memoria si la *page table* se encuentra en memoria:
$$ C = 2M$$
donde $M$ es el costo de acceso a memoria.

Costo de un acceso efectivo a memoria si la [[#Page Table]] se encuentra en memoria y además se posee de un TLB.
$$C = p(T + M) + (1-p)(T + 2M)$$
donde $M$ es el costo de acceso a memoria, $T$ el costo de acceso a memoria del TLB y $p$ la probabilidad de realizar un *hit*.

## Asignación de *Frames*
- Asignación Equitativa: Se dividen la cantidad de *frames* entre los proceso que se encuentran en ejecución.
- Asignación Proporcional: Se dividen la cantidad de *frames* entre los proceso que se encuentran en ejecución según el uso de memoria.

## Algoritmos de Reemplazo
Cuando se necesita cargar en memoria un *page* y no existe un *frame* disponible, se utiliza un *algoritmo de reemplazo* que se encargará de:
1. Seleccionar un *frame* para hacer el *swapping*.
2. *Swap out* del *page* correspondiente al *frame* seleccionado.
3. Invalidar los bits de validación correspondientes al *frame* seleccionado.
3. *Swap in* del *page* que generó *page fault*. 
4. Ajustar *page table* del proceso entrante.

>[!quote] Belady's Anomaly
>Agregar más *frames* podría aumentar el número de *page faults* con cierto tipos de *algoritmos de reemplazo*.

Los *algoritmos de reemplazo* pueden ser clasificados de la siguiente manera:
- Reemplazo global: Un proceso reemplaza un *frame* cualquiera, inclusive si es utilizado por otro proceso.
- Reemplazo local: Un proceso reemplaza únicamente los *frames* que tiene asignado.

### FIFO
Algoritmo de reemplazo que cumple con el principio *FIFO (first in, first out).*

### Reemplazo Óptimo
TODO

### Second Chance
TODO

### Not Recently Used
El algoritmo *not recently used (NRU)* es una variante mejorada de [[#Second Chance]]. Se asignan dos bits $r, m)$ a cada pagina. Donde $r$ vale $1$ si hubo una lectura reciente sobre la pagina y $m$ vale $1$ si se realizó una modificación reciente sobre la pagina. Por lo tanto, surgen 4 clases:
1. $00$ recientemente no hubieron modificaciones ni lecturas.
2. $01$ recientemente no hubieron modificaciones pero si lecturas.
3. $10$ recientemente hubieron modificaciones pero no lecturas.
4. $11$ recientemente hubieron modificaciones y lecturas.
El algoritmo selecciona como "victima" a una pagina de las primeras clases, pues al no haber modificaciones recientes, no sera necesario actualizar la pagina dentro del *swap space*.

### Least Recently Used
El algoritmo *least recently used (LRU)*, se encarga de reemplazar la pagina que produjo un *page fault* por la última pagina usada.

No cumple con *Belady's Anomaly*. Sea $\{f_0, f_1, ..., f_m\}$ el conjunto de *frames* y $\{p_0, p_1, ..., p_n\}$ el conjunto de *pages* (ordenadas de *más recientes* a *menos recientes*) con $n > m$, donde $A =\{(f_0, p_0), (f_1, p_1), ..., (f_m, p_m)\}$ el conjunto de asignaciones. Entonces, al agregar un nuevo *frame* $f_{m+1}$ el nuevo conjunto de asignaciones será $A' = A \cup \{(f_{m+1}, p_{m+1})\}$. Por ende, al agregar más *frames* no se podrán producir más *page faults* de los que se producían anteriormente.

## Page Trashing
También conocido como *hiperpaginación*, sucede cuando un proceso tiene en uso más *frames* de los que se encuentran en memoria principal se producirán más *page faults*. Lo que conlleva a que probablemente tenga más tiempo resolviendo *page faults* que usando el CPU. De esta forma, degradando el rendimiento del sistema.

### Working-Set
El *working-set* es una estrategia para afrontar [[#Page Trashing]] haciendo uso del *principio de localidad*.

El tamaño del *working-set* de un proceso varía durante el tiempo, y se define como el conjunto de *frames* que fueron usados en los últimos $t$ segundos por dicho proceso. Si este tamaño es mayor a la cantidad de *frames* que dispone el sistema, entonces, el proceso sufrirá de [[#Page Trashing]].