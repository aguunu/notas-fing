El *DNS (Domain Name System)* es una base de datos distribuida implementada de forma jerárquica en varios servidores. Los servicios principales de un DNS:
- Traducción de un *host name* a su *dirección IP* asociada.
- *host aliasing*
- Mail server aliasing
- Load Distribution: Varias direcciones IP corresponden a un *host name*.

La jerarquía esta dividida en los siguientes niveles:
1. **Root Servers**: Estos servidores almacenan información sobre las ubicaciones de los servidores de nombres de dominio de nivel superior (TLD) y ayudan a dirigir las consultas de resolución de DNS hacia los servidores TLD adecuados.
2. **Top-Level Domain Servers (TLD)**: Estos servidores almacenan información sobre los *authoritative servers* asociados al dominios específicos dentro de su extensión.
3. **Authoritative Servers**: Los servidores autorizados son servidores DNS que contienen la información real y actualizada sobre un dominio específico.

![[Drawing 2023-08-03 21.56.07.excalidraw|center]]


>[!question] ¿Porqué no centralizar el DNS?
>El *Domain Name System* difícilmente podría ser centralizado. Pues no es escalable debido a los siguientes factores:
>- Ante una falla, se caería el sistema en su totalidad.
>- Gran volumen de trafico.
>- Base de Datos distante.
>- Mantenimiento.
>
>*Nota: Comcast DNS servers resuelven 600 mil millones de consultas por día.*


## Local DNS
Cuando un *host* realiza una consulta de DNS, esta es enviada al *local DNS server*. Luego, el *local DNS server* responde dicha consulta; usando el *local cache* del *local DNS server*, o enviando dicha consulta a un *root DNS server.* En caso de que la consulta sea enviada a un *root DNS server*, esta se resuelve de forma jerárquica, de forma *iterativa* o *recursiva*.

>[!warning] 
>En caso de que la consulta sea resuelta por cache, existe la posibilidad de que el valor asociado este *out of date*, es decir, sea invalido. Por lo tanto, el cache eliminará una entrada después de un tiempo llamado **TTL**.

![[Drawing 2023-08-04 17.04.51.excalidraw|center]]
## Resource Record
Los registros de un DNS (*resource record*), se almacenan respetando en el siguiente formato: ($\texttt{name}$, $\texttt{value}$, $\texttt{type}$, $\texttt{ttl}$).

- $\texttt{type=A} \rightarrow$ referencia a una dirección de host.
- $\texttt{type=NS} \rightarrow$ referencia a un servidor autoritativo para dicho dominio.
- $\texttt{type=CNAME} \rightarrow$ referencia al nombre canónico para el alias. *(ej. el nombre canónico de www.ibm.com es  servereast.backup2.ibmcom).*
- $\texttt{type=MX} \rightarrow$  referencia a un servidor [[Electronic Mail|EMAIL]] para dicho dominio.

## DNS Protocol
Los mensajes de consulta y respuestas poseen el siguiente formato.
![[Drawing 2023-08-04 18.10.17.excalidraw|center]]
- $\texttt{ID} :$ identificador de 16 bits asignado por el programa que genera cualquier tipo de consulta. Este identificador se copia  la respuesta correspondiente y puede ser utilizada por el solicitante  para comparar las respuestas a las consultas pendientes.
- $\texttt{QR (Flag)} :$ especifica si el mensaje es un consulta (0), o una respuesta (1).
- $\texttt{Authoritative Answer (AA Flag)} :$ este bit es válido en respuestas, y especifica que el servidor  que responde es autoritativo para el nombre de dominio en la sección $\texttt{Questions}$.
- $\texttt{Recursion Desired (RD Flag)} :$ este bit puede establecerse en una consulta y se copia en la respuesta. Especifica que el emisor desea que la consulta sea recursiva.
- $\texttt{Recursion Available (RA Flag)} :$ se establece en una respuesta, indica si el soporte de consultas recursivas es disponible en el servidor de nombres.
- $\texttt{Question Section} :$ contiene las consultas realizadas siguiendo el formato $(\texttt{class, type, value})$.
- $\texttt{Answer Section} :$ contiene [[#Resource Record|RRs]] que responden a la $\texttt{Question Section}$.
- $\texttt{Authority Section} :$ contiene [[#Resource Record|RRs]] que apuntan a un servidor autoritativo.
- $\texttt{Additional Information} :$ contiene [[#Resource Record|RRs]] adicionales, es decir, que no se consideran respuesta a la $\texttt{Question Section}$.

*Notar: para saber si una consulta se produjo de forma recursiva se realiza $\texttt{RD} \land \texttt{RA}$ en la respuesta, siendo recursiva si el resultado es $1$.*

>[!example] 
>Supongamos que empezamos un nuevo emprendimiento "Segurovich" y deseamos agregar nuestro sitio al DNS.
>
>Debemos registrar el nombre `segurovich.com` en un *DNS registrar* *(ej. Network Solutions).* Proveerle el nombre e IP de nuestro *authoritative name server* (primario y secundario). Luego, el *DNS registrar* inserta los registros (RRs) de tipo `NS`, `A` dentro de un servidor .com TLD; `(segurovich.com, dns1.segurovich.com, NS)`, `(dns1.segurovich.com, 212.212.212.1, A)`.