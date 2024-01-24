El *EMAIL (Electronic Mail)* tiene tres componentes principales:
- User Agents
- Mail Server
- SMTP

1. El emisor compone un *e-mail* destinado a un destinatario.
2. El **User Agent** *(ej. Outlook, Thunderbird, iPhone Mail Client)* del emisor se encarga de enviar el mensaje a su servidor mail usando el protocolo SMTP; donde el mensaje es colocado en una cola de mensajes.
3. Dicho servidor inicia una conexión [[TCP]] con el servidor mail del destinatario y envía el mensaje por la conexión [[TCP]] iniciada.
4. El servidor mail del destinatario coloca el mensaje en la casilla del destinatario.
5. El destinatario podrá invocar su *User Agent* para leer el mensaje recibido.
## SMTP
Se encarga de enviar los mensajes entre los servidores emisores y los servidores receptores de mail. Utiliza el protocolo TCP para el envío confiable de mensajes de mail desde el servidor cliente al “servidor” a través del puerto 25, a través de una transferencia directa.
El envío de mail consiste de tres fases:
1. Handshaking
2. Transferencia de mensajes
3. Cierre

```
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipent ok
C: DATA
S: 345 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

## Protocolos de Acceso a Mail
Si el cliente receptor desea acceder al mensaje, necesita utilizar un Protocolo de Acceso a Mail, el cual recupera del servidor. Entre ellos se destacan *POP*, *IMAP*, *HTTP*.