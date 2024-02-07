El *host* es el encargado de dividir los datos a enviar en chunks de tamaño fijo mediante [[Network#Packet-Switching|Packet-Switching]]. Luego, la red envía dichos *data-packets* desde un nodo a otro mediante una ruta de [[Enlace|Enlaces]] cuyos extremos son los hosts origen y desino.

## Packet Delay
El tiempo de retraso de un paquete desde un nodo a otro mediante un *único* enlace se calcula como
$$d_{nodal}=d_{proc}+d_{queue}+d_{trans}+d_{prop}$$
- $d_{proc}$ (Node Processing Delay): Tiempo de procesamiento del nodo sobre el paquete. *(Chequear errores, recalcular [[Detección y Corrección de Errores#Checksum|Checksum]], determinar la salida del enlace, etc.)*
- $d_{queue}$ (Queue Delay): Tiempo de espera en la cola del nodo. Nota: Sea $a$ la velocidad de arribo de paquetes, $L$ el tamaño de paquete, $R$ la velocidad de transmisión *(bandwidth)*, entonces, $$\texttt{Traffic Intensity} = \frac{L\cdot a}{R}$$ Además, podemos observar que $$
\frac{L \cdot a}{R}
\begin{cases}
\approx 0:  & \textit{avg $d_{queue}$ pequeño} \\
\rightarrow 1:, & \textit{avg $d_{queue}$ grande} \\
> 1:, & \textit{avg $d_{queue}$ infinito} \\
\end{cases}
$$
- $d_{trans}$ (Transmission Delay): Tiempo de "colocación" de los bits en el [[Enlace]]. Sea $L$ el tamaño de un paquete, $R$ la velocidad de trasmisión *(bandwidth)*, entonces, $d_{trans}=\frac{L}{R}$.
- $d_{prop}$ (Propagation Delay): Tiempo que tarda en propagarse los bits desde un extremo a otro dentro del [[Enlace]]. Sea $d$ el largo del enlace, $s$ la velocidad de propagación del medio, entonces, $d_{prop}=\frac{d}{s}$.

## Packet Loss
Dado que el buffer de la cola de cada nodo tiene capacidad finita, puede suceder que cuando un paquete arriba en cierto nodo, este sea descartado en caso de no haber espacio disponible en el buffer. *Con ciertos mecanismos que permiten detectar perdidas, el nodo origen, podría intentar reenviar el paquete al detectar la perdida.*
