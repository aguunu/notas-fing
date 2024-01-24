*OSPF (open shortest path first)* se basa en el protocol Link-State. Es un protocolo de enrutamiento intra-dominio, que permite el [[Enrutamiento Jerárquico]], dividiendo un [[Dynamic Routing#Autonomous System|AS]] en varias zonas.

Algunas de las funcionalidades avanzadas incluidas en OSPF son las siguientes:
- Seguridad: Los intercambios entre routers OSPF pueden ser autentificados. Con esto solo pueden participar en el protocolo OSPF los routers de confianza del sistema autónomo. Por defecto, los paquetes OSPF entre routers no son identificados y podrían ser alterados. Pueden configurarse dos tipos de autenticación: simple y MD5.
- Varias rutas de igual coste: cuando varias rutas de un destino tienen el mismo coste, OSPF permite utilizar varias rutas.
- Soporte integrado para enrutamiento de unidifusión y por multidifusión: OSP multidifusión añade extensiones simples a OSPF para proporcionar enrutamiento por multidifusión.
- Soporte para añadir una jerarquía dentro de un mismo dominio de enrutamiento.

Se tienen dos niveles de jerarquía, *local area* y *backbone*. Los anuncios solo ocurren en *local area*. Cada nodo tiene una topología detallada de áreas, solo sabe direcciones a redes en otras áreas.
- *boundary routers*: actúan como límite entre diferentes dominios de enrutamiento, como la conexión entre dos [[Dynamic Routing#Autonomous System|AS]]. Gestionan la información de enrutamiento entre dominios y realizar tareas como la redistribución de rutas.
- *backbone routers*: su función principal es facilitar la conectividad entre las diferentes áreas OSPF al actuar como el núcleo de la red OSPF.
- *area border routers*: conectan áreas diferentes dentro de un [[Dynamic Routing#Autonomous System|AS]] OSPF.
- *internal routers*: residen completamente dentro de una única área OSPF y se encargan de construir y mantener la base de datos de enrutamiento de su área.

![[Drawing 2023-12-10 16.20.19.excalidraw|center]]