
- *broadcast routing*: mecanismo para enviar un paquete desde un nodo a *todos* los demás nodos de la red.
- *multicast routing*: mecanismo para enviar un paquete desde un nodo a un *subconjunto* de los demás nodos de la red.

## Broadcast Routing
Representando una red como un grafo $G=(V, E)$ donde $V, E$ representan los conjuntos de nodos y enlaces respectivamente. Además, $|V|=N$.

- *n-way-unicast*: simplemente se crean $n$ copias del paquete y estas son enviadas a cada uno de los $n$ nodos destino. *Notar: este método es ineficiente, ya que el nodo origen debe conocer las $n$ direcciones destino y además algunos enlaces podrán recibir tráfico duplicado.*

- *uncontrolled flooding*: el nodo origen envía una copia a todos sus *vecinos*. Cuando un nodo recibe un mensaje broadcast, este lo reenvía a todos sus vecinos (excepto por el vecino que envió dicho paquete). *Notar: si el grafo posee ciclos, una o más copias llegarán a algunos nodos. Además, puede ocurrir el fenómeno de __broadcast storm__, donde en ciertos casos se generen copias de forma exponencial sobre la red.*

- *controlled flooding*: a diferencia de *uncontrolled flooding*, se agrega un *broadcast sequence number* para identificar el mensaje de broadcast. Luego, cada nodo mantiene una lista de *(source address, sequence number)* para   chequear si ya había recibido dicho mensaje. 
    Otro método es utilizar la técnica *reverse path forwarding*, cuando un nodo recibe un mensaje broadcast, este lo reenvía a todos sus vecinos (excepto al vecino que envió el mensaje) ==solo si el paquete llegó por el enlace que esta en el camino más corto hacia el nodo origen.== *Notar: a pesar de que ambas técnicas evitan __broadcast storm__, no resuelve el problema de paquetes duplicados.*

- *spanning-tree*: cuando un nodo desea enviar un mensaje broadcast, este calcula el *spanning-tree* $G'$ de la red y envía una copia del mensaje a todos sus *vecinos* respecto a $G'$. Cuando un nodo recibe un mensaje broadcast, este lo reenvía a todos sus vecinos (excepto por el vecino que envió dicho paquete). *El método para generar el spanning-tree[^spanning-tree] varía según las necesidades. Por ejemplo, se podría optar por generar el minimum-spannning-tree[^minimum-spanning-tree].*

## Multicast Routing
Un paquete multicast es direccionado mediante *address indirection*, esto es, a cada paquete se le asigna un identificador para representar al grupo de receptores, este identificador se lo conoce como una dirección IP clase D y hace referencia a un *multicast-group*. 

- *group-shared tree*: un único árbol es creado para enviar el tráfico desde el origen a cada uno de los miembros del grupo.
- *source-based tree*: cada miembro que envía tráfico al grupo crea su propio árbol.

[^spanning-tree]: Un *spanning tree* de un grafo $G=(V, E)$, es un grafo $G'=(V,E')$ de forma que $E' \subseteq E$, $G'$ es conexo, no contiene ciclos y contiene todos los nodos originales de $G$.
[^minimum-spanning-tree]: El *minimum-spanning-tree* de un grafo $G=(V, E)$ es aquel *spanning-tree*[^spanning-tree]  de $G$ que minimiza la suma de los costos de los vertices.