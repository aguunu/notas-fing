## Autonomous System
Un *autonomous system (AS)* es cualquier conjunto de routers o redes bajo un único control administrativo. 
## Interior Gateway Protocol
Los protocolos *IGP (Interior Gateway Protocol)* son usados para compartir rutas dentro de un mismo [[#Autonomous System|AS]].
- RIP *(distance vector)*
- EIGRP *(distance vector)*
- [[OSPF]] *(link state)*
- IS-IS *(link state)*

## Exterior Gateway Protocol
Los protocolos *EGP (Exterior Gateway Protocol)* son usados para compartir rutas entre distintos [[#Autonomous System|ASs]].
- [[BGP]]

## Link State Routing


## Distance Vector Routing
Se basan en la ecuación de *Bellman-Ford* *(dynamic programming).*
Sea $D_x(y)$ es el costo del camino menos costoso de $x$ a $y$, entonces:
$$D_x(y) = min\{c_{x,v} + D_v(y)\}$$
La idea principal de los *distance vector algorithms* es que cada nodo envíe a sus vecinos cada cierto tiempo su vector distancia. Luego, cuando un nodo recibe un vector distancia, actualiza su vector distancia utilizando la ecuación de *Bellman-Ford*.

```
1. wait for (change in local link
cost or msg from neighbor)

2. recompute my DV estimates
using DV received from neighbor

3. if my DV to any destination
has changed, send my new DV
my neighbors, else do nothing.
```

>[!info] 
>Un nodo no tiene porque saber el camino completo, sino por donde enviar el tráfico entrante.

***

Al comparar  [[#Link State Routing]] y [[#Distance Vector Routing]] obtenemos las siguientes diferencias:

Link State|Distance Vector
---|---
Conocimiento de la topología en su totalidad.|Conocimiento únicamente del *next-hop*.
Menor consumo de RAM/CPU.|Mayor consumo de RAM/CPU.
Convergencia lenta.|Convergencia rápida.
