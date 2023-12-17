Los enlaces tienen un *Maximum Transmission Unit (MTU)*, que es el tamaño máximo posible de un [[Ethernet#Ethernet Frame|Frame]]. De esta forma, un datagrama IP es dividido en fragmentos dentro de la red. Así, un datagrama se convierte en múltiples datagramas, que son reensamblados únicamente cuando llegan al destino final.

>[!example] 
>Se enviará el datagrama `[lenght=4000|id=x|fragflag=0|offset=0|...]` por un enlace cuyo MTU es de 1.500 bytes.
>En primer lugar, asumiendo que el tamaño de la cabecera IP es de 20 bytes, entonces tenemos una carga útil de 1.500 bytes - 20 bytes = 1.480 bytes. Por ende, el datagrama original será fragmentado en los siguientes fragmentos:
>1. `[lenght=1500|id=x|fragflag=1|offset=0|...]`
>2. `[lenght=1500|id=x|fragflag=1|offset=185|...]`
>3. `[lenght=1040|id=x|fragflag=0|offset=370|...]`
>   
>   El campo $\texttt{offset}$ indica a que posición dentro del datagrama pertenece este fragmento. Este campo se mide en unidades de 8 bytes. El $\texttt{offset}$ del primer fragmento siempre es igual a 0. *Notar que el $\texttt{offset}$ del segmento i-esimo se puede calcular como $\texttt{offset}_i=i \cdot \frac{CU}{8}$ siendo $CU$ la carga útil del enlace.*
