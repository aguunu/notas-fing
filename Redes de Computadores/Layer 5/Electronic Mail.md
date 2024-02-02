## SMTP
SMTP (Simple Mail Transfer Protocol) permite a los servidores que implementen dicho protocolo intercambiar correos electrónicos entre ellos. *Importante: SMTP no es un protocolo de recuperación de correos, sino que es un protocolo de entrega.

## Email Client
Un *email client (agent)* es un software utilizado por el usuario donde se encuentra implementado el protocolo `SMTP` al igual que algunos protocolos de recuperación como `POP` e `IMAP`. Los *email clients* permiten al usuario enviar, recibir y responder correos. *Outlook, Gmail y Thunderbird son ejemplos de dicho software.*

## Mail Server
Los *mail servers* conforman el núcleo de la infraestructura del correo electrónico. Cada usuario posee su *mailbox* ubicado en un *mail server* administrado por su proveedor de correo electrónico.

El envío de un correo consiste de los siguientes pasos:
1. El emisor indica el correo del receptor, compone un mensaje y lo "envía".
2. El *email client* envía el correo a uno de los *mail servers* del proveedor del emisor.
3. Se inicia una conexión [[TCP]] entre uno de los *mail servers* del emisor y uno de los *mail servers* del receptor. *Nota: puede usar servidores SMTP intermediarios, aunque no es una practica común.*
4. Se realiza un *SMTP handshaking* y el mensaje es enviado desde un *mail server* al otro.
5. El *mail server* del receptor recibe el mensaje y lo coloca en el *mailbox* del receptor.
6. Finalmente, el receptor invoca a su *email client* y extrae el correo de su *mailbox*.

>[!error] 
>Si una vez que el correo se encuentra en el *mail server* del emisor, y este no puede ser enviado, el correo se colocará en una *message queue* donde se intentará retransmitir o se le avisará al emisor sobre el fallo.

```Handshake
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
```

``` Header
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr... Sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... Recipent ok
```

```Message
C: DATA
S: 345 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

>[!tip] 
>Para obtener la IP de un mail server del proveedor `fing.edu.uy` bastaría con realizar una consulta [[DNS]] del registro `MX` sobre dicho dominio.
