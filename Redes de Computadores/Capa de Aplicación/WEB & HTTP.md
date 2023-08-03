Cada página web consiste en un archivo base HTML que incluye referencias a otros objetos, cada uno de ellos direccionable por una URL.

>[!example]
>Sea la URL `www.someschool.edu/someDept/pic.gig`, donde el `www.someschool.edu` indica el nombre del host, y `/someDept/pic.gig` indica el nombre del camino.

## HTTP
HTTP (Hyper Text Transfer Protocol). Es el protocolo de la [[Capa de Aplicación]] de la Web, y se basa en el [[Capa de Aplicación#Modelo de Aplicaciones|Modelo Cliente-Servidor]], donde el cliente es el buscador que solicita, recibe y “muestra” los objetos de la web. Y el servidor es el servidor web, que recibe las peticiones y envía los objetos como respuesta.

HTTP utiliza [[TCP]] como su protocolo de transporte. El cliente inicia una conexión [[TCP]] (crea el [[Capa de Aplicación#Sockets|Socket]]) con el servidor, en el puerto 80. El servidor recibe y acepta la conexión [[TCP]] del cliente. Los mensajes HTTP (mensajes del protocolo de la capa de aplicación) son intercambiados entre el cliente HTTP y el servidor HTTP. *Nota: Como se utiliza [[TCP]] como protocolo, se puede garantizar que tanto los mensajes enviados como los recibidos llegaran intactos.* Por otra parte, el protocolo HTTP no mantiene ninguna información sobre las peticiones HTTP de los clientes **(stateless)**.
- **HTTP Persistente**: Como máximo un objeto es enviado a través de la conexión TCP.
  Se define **RTT (Round Trip Time)** como el tiempo que tarda un paquete pequeño en viajar desde el cliente al servidor y volver.
  ![[Drawing 2023-07-31 18.06.54.excalidraw|center]]
- **HTTP No-Persistente**: En este tipo de conexión el servidor deja la conexión abierta después de enviar la respuesta, por lo que los mensajes HTTP subsecuentes entre el mismo cliente/servidor se envían a través de la misma conexión abierta.
### HTTP Request Message
Métodos HTTP/1.0: `GET`, `POST`, `HEAD`.
Métodos HTTP/1.1: `GET`, `POST`, `HEAD`, `PUT`, `DELETE`.

```
GET /index.html HTTP/1.1\r\n
Host: www.fing.edu.uy\r\n
User-Agent: Firefox/3.6.10\r\n
Accept: text/html, application/xhtml+xml\r\n
Accept-Language: en-Us, en;q=0.5\r\n
Accept-Encoding: gzip,deflate\r\n
Accept-Charset: ISO-8859-1,utf-8;q=0.7\r\n
Keep-Alive: 115\r\n
Connection: keep-alive\r\n
\r\n
```

### HTTP Response Message

```
HTTP/1.1 200 OK
Date: Tue, 08 Sep 2020 00:53:20 GMT
Server: Apache/2.4.6 (CentOS)
    OpenSSL/1.0.2k-flips PHP/7.4.9
    mod_perl/2.0.11 Perl/v5.16.3
Last-Modified: Tue, 01 Mar 2016 18:57:50 GMT
ETag "a5b-52d015789ee9e"
Accept-Ranges: bytes
Content-Length: 2651
Content-Type: text/html; charset=UTF-8
\r\n
data data ... data
```

### Cookies
Los sitios webs y los navegadores utilizan *cookies* para poder mantener un estado entre las transacciones. Una *cookie* es asignada a cierto cliente por el servidor, luego, a través de una *HTTP response*, el servidor devuelve la *cookie* a dicho cliente. El cliente utilizará la *cookie* otorgada en futuras *HTTP requests* (colocándola en el *header* de la *request*), de esta forma, logrando mantener el estado que esta siendo administrado por el servidor.

>[!info] 
>Una vez que el cliente recibe una *cookie* de cierto sitio web, esta es administrada y almacenada por el navegador de cliente, para que luego pueda ser usada en un futuro.