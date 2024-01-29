El protocolo BGP (Border Gateway Protocol) es el protocolo de ruteo por defecto entre dominios.
En BGP un [[Dynamic Routing#Autonomous System|AS]] es identificado mediante un número global, llamado *AS number* (ASN). Este protocolo provee a cada AS un medio para:
- eBGP: obtener la información de alcance de la subred a partir de los AS vecinos.
- iBGP: propagar la información de alcance a todos los routers internos al AS.

En BGP, los pares de routers intercambian la información de ruteo mediante conexiones [[TCP]]. En general, existe una conexión TCP por cada enlace que conecta directamente dos routers en dos AS distintos. Además, hay también una conexión TCP semipermanente entre los routers dentro del AS.
Para cada conexión TCP, los dos routers que participan son llamados *BGP peers*, y la conexión TCP, acompañada de todos los mensajes BGP enviados a través de esta es llamada *BGP session*. Estos mensajes se utilizan para comunicar los caminos a diferentes prefijos de redes de destino, donde cada prefijo representa una subred o una colección de subredes.

Además de anunciar la subred destino, también se anuncian ciertos atributos, entre ellos se destacan:
- $\texttt{AS-PATH}$: lista de los ASs a través de los cuales el aviso para ese prefijo ha pasado. Cuando un prefijo es pasa por un AS, este agrega su ASN a este atributo. La utilidad de este atributo es evitar loops, ya que, si un router detecta que su AS ya está en la lista, lo ignora. 
- $\texttt{NEXT-HOP}$: indica el router dentro del next-hop AS que se debe usar para llegar al destino. (Pueden ser múltiples enlaces desde el AS actual al next-hop AS).

>[!info] 
>Los routers que reciben anuncios BGP, utilizan una *policy* para aceptar/rechazar la ruta. *(ej. nunca enrutar trafico mediante AS 100).*

## Mensajes BGP
Los mensajes BGP son intercambiados entre peers sobre conexiones TCP. Los mensajes son:
- $\texttt{OPEN}$: abre la conexión TCP hacia el peer y autentica al emisor.
- $\texttt{UPDATE}$: avisa un nuevo camino, o retira el viejo.
- $\texttt{KEEPALIVE}$: mantiene la conexión activa en ausencia de UPDATES; también solicitudes OPEN de los ACKs.
- $\texttt{NOTIFICATION}$: reporta errores en mensajes anteriores. Usado también para cerrar la conexión