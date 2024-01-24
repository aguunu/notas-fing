Es la capa cuyo objetivo es brindarle soporte a las aplicaciones de red *(ej. FTP, SMTP, HTTP, DNS, P2P)*.

## Modelo de Aplicaciones
- Modelo Cliente-Servidor: En este modelo, las tareas se reparten entre el cliente[^1] y servidor.[^2] *Nota: Este tipo de arquitectura no permite una comunicación cliente-cliente directamente*.
- Modelo Peer To Peer (P2P): En este modelo, no se tiene un servidor[^2]. En su lugar, se tiene una comunicación directa con *peers*, los cuales son *end systems* que están intermitentemente conectados y que poseen una dirección IP dinámica. Estos dispositivos son controlados por los usuarios y no dependen de un servidor dedicado.
- Modelo Híbrido: Consiste en utilizar tanto un modelo P2P como una Cliente-Servidor.

## Comunicación entre Procesos
Un [[Procesos|Proceso]] en ejecución en cierto host se comunica mediante [[Inter Process Communication]] con procesos que se encuentran en el mismo host. Sin embargo, en distintos hosts, se comunican intercambiando mensajes por la red.

### Sockets
Es una interfaz que permite a la comunicación de procesos que se encuentran en distintos hosts mediante la emisión y recepción de mensajes.

Los únicos controles que se hacen desde el *socket* son la elección del protocolo de transporte y la habilidad de corregir algunos parámetros.

### Direccionando Procesos
Para que la comunicación sea posible, se necesita identificar el host, lo cual se realiza mediante la dirección IP de este. Luego, una vez identificado el host, se necesitará identificar el proceso. Por este motivo, el proceso tendrá asignado un *port number* dentro del host para poder ser identificado.

>[!example] 
>El puerto 80 suele estar asociado al servidor HTTP. Por ende, si se desea mandar un mensaje HTTP a fing.edu.uy, se necesita la IP (164.73.32.20) y el número de puerto 80.

## Servicios en la Red
Existen dos tipos de [[Protocolo]] para los servicios/aplicaciones, los de **Dominio Público** *(ej. HTTP, SMTP)* y los **Protocolos de Propietario** *(ej. Skype)*. Algunas características que se deben tener en cuenta en una aplicación de red son:
- Data Loss
- Time
- Throughput
- Security

>[!example] 
>En una aplicación de mensajería instantánea, no se puede permitir *data loss*, además el tiempo de retraso no deberá pasar de 500ms. Mientras que el [[Network#Throughput|Throughput]] es elástico, pues con un aproximado de 20kbps la aplicación funcionará correctamente. Además, los datos deberán ser encriptados, ya que los mensajes podrían contener información confidencial.

[^1]: Un cliente es un host que se comunica con un servidor. Posee una dirección IP dinámica.
[^2]: Un servidor es un host que se mantiene encendido constantemente con una dirección IP permanente.
