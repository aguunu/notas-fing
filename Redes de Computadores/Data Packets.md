El *host* es el encargado de dividir los datos a enviar en chunks de tamaño fijo mediante [[Network#Packet-Switching|Packet-Switching]]. Luego, la red envía dichos *data-packets* desde un nodo a otro mediante una ruta de [[Network#Enlace Físico|Enlaces Físicos]] cuyos extremos son los hosts origen y desino.

## Packet Delay
El tiempo de retraso de un paquete desde un nodo a otro mediante un único enlace se calcula como
$$d_{nodal}=d_{proc}+d_{queue}+d_{trans}+d_{prop}$$
- $d_{proc}$ (Node Processing Delay): Tiempo que invierte el *nodo* para chequear errores y determinar la salida del enlace.
- $d_{queue}$ (Queue Delay): Tiempo de espera en la salida del enlace.
- $d_{trans}$ (Transmission Delay): Tiempo de "colocación" de los bits en el enlace físico. Sea $L$ el largo del paquete, y $R$ la velocidad de trasmisión, entonces, $d_{trans}=\frac{L}{R}$.
- $d_{prop}$ (Propagation Delay): Tiempo que tarda en propagarse los datos desde un extremo a otro dentro del enlace físico. Sea $d$ el largo del enlace físico, y $s$ la velocidad de propagación del medio, entonces, $d_{prop}=\frac{d}{s}$.

>[!bug] Perdida de Paquetes
>Dado que el *buffer* de la *queue* de un *nodo* tiene capacidad finita, puede darse el caso de que un paquete entrante al nodo se pierda al no haber espacio disponible en el *buffer*. Sin embargo, es posible que el paquete perdido sea retrasmitido por el nodo anterior o el *End System* origen.
