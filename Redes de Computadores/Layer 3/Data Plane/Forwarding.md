Consiste en enviar los paquetes mediante la interfaz correspondiente utilizando una *forwarding table* donde se examina el *IP header* asociado al paquete y se indexa el campo IP destino en dicha tabla, reenviando el paquete por la interfaz correspondiente.

|Network|Interface|Gateway|
|--|--|--|
|0.0.0.0/0|$\texttt{eth0}$ |101.101.101.1|
|192.168.4.0/24|$\texttt{eth1}$ |$\texttt{DC}$ |
|100.100.2.128/27|$\texttt{eth1}$ |192.168.4.1|

>[!note] 
>En caso de suceda más de un match, se selecciona la entrada de prefijo más largo.