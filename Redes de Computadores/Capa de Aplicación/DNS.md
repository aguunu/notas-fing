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
## DNS Records
Los registros de un DNS **(RR)**, se almacenan respetando el siguiente formato: `(name, value, type, ttl)`.

- `type=A`
	- `name` referencia a un *hostname/dominio.*
	- `value` IP asociada a `name`.
- `type=NS`
	- `name` referencia a un *host* *(ej. fing.com).*
	- `value` es el *hostname* del *authoritative name server* asociado a `name`.
- `type=CNAME`
	- `name` es un alias del objeto.
	- `value` es el nombre canónico asociado a `name` *(ej. www.ibm.com es realmente servereast.backup2.ibmcom).* *Nota: Cuando el DNS consulta un alias y encuentra un CNAME asociado, luego, consultará  dicho nombre canónico.*
- `type=MX`
	- `name` referencia a un *hostname/dominio.*
	- `value` es el nombre de servidor [[Electronic Mail]] asociado a `name`.

## DNS Protocol
Los mensajes de consulta y respuestas poseen el mismo formato.
![[Drawing 2023-08-04 18.10.17.excalidraw|center]]
>[!example] 
>Supongamos que empezamos un nuevo emprendimiento "Segurovich" y deseamos agregar nuestro sitio al DNS.
>
>Debemos registrar el nombre `segurovich.com` en un *DNS registrar* *(ej. Network Solutions).* Proveerle el nombre e IP de nuestro *authoritative name server* (primario y secundario). Luego, el *DNS registrar* inserta los registros (RRs) de tipo `NS`, `A` dentro de un servidor .com TLD; `(segurovich.com, dns1.segurovich.com, NS)`, `(dns1.segurovich.com, 212.212.212.1, A)`.