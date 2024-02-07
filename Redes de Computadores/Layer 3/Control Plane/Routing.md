## Dynamic Routing
El *dynamic routing* se basa en la utilización de protocolos que implementan [[Routing Algorithms]] con el fin de automatizar el intercambio y la actualización de las tablas de enrutamiento de cada uno de los routers. Estos protocolos comparten las información sobre la red de forma automática con los routers cercanos, lo que hace que su utilización sea recomendada para redes grandes.

## Static Routing
El *static routing* es aquel en el que el administrador de la red debe encargarse de configurar manualmente cada uno de los [[Router|Routers]] que forman la misma. Por lo general, se utiliza principalmente en redes con una cantidad pequeña de routers, las cuales tienen un solo *gateway*.

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

