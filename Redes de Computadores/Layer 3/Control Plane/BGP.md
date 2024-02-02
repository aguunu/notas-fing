El protocolo BGP (Border Gateway Protocol) es el protocolo de ruteo por defecto entre dominios.
En BGP un [[Dynamic Routing#Autonomous System|AS]] es identificado mediante un número global, llamado *AS number* (ASN). Este protocolo provee a cada AS un medio para:
- $\texttt{eBGP}$: obtener la información de alcance de la subred a partir de los AS vecinos.
- $\texttt{iBGP}$: propagar la información de alcance a todos los routers internos al AS.

En BGP, los pares de routers intercambian la información de ruteo mediante conexiones [[TCP]]. En general, existe una conexión TCP por cada enlace que conecta directamente dos routers en dos AS distintos. Además, hay también una conexión TCP semipermanente entre los routers dentro del AS.
Para cada conexión TCP, los dos routers que participan son llamados *BGP peers*, y la conexión TCP, acompañada de todos los mensajes BGP enviados a través de esta es llamada *BGP session*. Estos mensajes se utilizan para comunicar los caminos a diferentes prefijos de redes de destino, donde cada prefijo representa una subred o una colección de subredes.

El protocolo BGP permite anunciar una ruta compuesta por un prefijo de red y ciertos atributos, entre ellos se destacan:
- $\texttt{AS-PATH}$: lista de ASs a través de los cuales el aviso para ese prefijo ha pasado. Cuando un AS anuncia una ruta, este agrega su ASN a este atributo. Además, en $\texttt{eBGP}$, si un router detecta que su AS está en la lista, lo ignora para evitar loops. *Notar: en $\texttt{iBGP}$ este atributo no se utiliza para detectar ciclos ya que no varia dentro del AS.*
- $\texttt{NEXT-HOP}$: indica la dirección del router que inicia el $\texttt{AS-PATH}$. En $\texttt{eBGP}$, el router que anuncia cambia este valor a su propia dirección.

>[!info] 
>Los routers que reciben anuncios BGP, utilizan una *policy* para aceptar/rechazar la ruta. *(ej. nunca enrutar trafico mediante AS 100).*

## Route Selection
Si existen dos o más rutas al mismo prefijo, BGP ejecuta secuencialmente las siguientes reglas de desempate:
1. Se selecciona la ruta con valor $\texttt{local-pref}$ (preferencia local) más alto.
2. Se selecciona la ruta con atributo $\texttt{AS-PATH}$ más corto.
3. Se selecciona la ruta con atributo $\texttt{NEXT-HOP}$ más cercano. *(hot-potato routing)*
4. Se selecciona la ruta que proviene del router con $\texttt{BGP ID}$ más bajo.

## Mensajes BGP
Los mensajes BGP son intercambiados entre peers sobre conexiones TCP. Los mensajes son:
- $\texttt{OPEN}$: abre la conexión TCP hacia el peer y autentica al emisor.
- $\texttt{UPDATE}$: avisa un nuevo camino, o retira el viejo.
- $\texttt{KEEPALIVE}$: mantiene la conexión activa en ausencia de UPDATES; también solicitudes OPEN de los ACKs.
- $\texttt{NOTIFICATION}$: reporta errores en mensajes anteriores. Usado también para cerrar la conexión.
