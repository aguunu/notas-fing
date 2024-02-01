*OSPF (open shortest path first)* es un protocolo de enrutamiento *link-state*. Además, de ser un *interior gateway protocol (IGP)*, que 

Un router ejecutando OSPF, emite información sobre el estado de los enlaces de forma periódica a todos los nodos de su AS (incluso si la información no varia).

Algunas de las funcionalidades avanzadas incluidas en OSPF son las siguientes:
- Los intercambios entre routers OSPF pueden ser autentificados. 
- Cuando existen multiples rutas de igual costo a un destino, OSPF permite usar varias rutas.
- Soporte de enrutamiento *unicast* y *multicast*.
- Permite [[Enrutamiento Jerárquico]], dividiendo un [[Dynamic Routing#Autonomous System|AS]] en varias zonas.

Se tienen dos niveles de jerarquía, *local area* y *backbone*. Los anuncios solo ocurren en *local area*. Cada nodo tiene una topología detallada de áreas, solo sabe direcciones a redes en otras áreas.
- *boundary routers*: actúan como límite entre diferentes dominios de enrutamiento, como la conexión entre dos [[Dynamic Routing#Autonomous System|AS]]. Gestionan la información de enrutamiento entre dominios y realizar tareas como la redistribución de rutas.
- *backbone routers*: su función principal es facilitar la conectividad entre las diferentes áreas OSPF al actuar como el núcleo de la red OSPF.
- *area border routers*: conectan áreas diferentes dentro de un [[Dynamic Routing#Autonomous System|AS]] OSPF.
- *internal routers*: residen completamente dentro de una única área OSPF y se encargan de construir y mantener la base de datos de enrutamiento de su área.

![[Drawing 2023-12-10 16.20.19.excalidraw|center]]