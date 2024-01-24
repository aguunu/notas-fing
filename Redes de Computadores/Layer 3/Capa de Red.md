La *network layer* consiste de dos principles funcionalidades *forwarding (data plane)* y *routing (control plane)*.

## Forwarding
Consiste en enviar los paquetes mediante la interfaz correspondiente utilizando una *forwarding table* examinando el cabezal IP del paquete.

|Network|Interface|Gateway|
|--|--|--|
|0.0.0.0/0|eth0|101.101.101.1|
|192.168.4.0/24|eth1|DC|
|100.100.2.128/27|eth1|192.168.4.1|

>[!info] 
>En caso de que suceda más de un *match*, se utiliza la entrada del prefijo más largo, enviando el paquete por la interfaz asociada.

## Routing
Los *routing algorithms* se utilizan para popular la *forwarding table*. Estos algoritmos determinan la ruta que tomarán los paquetes para llegar a destino.

## Redes de Datagramas
Un paquete es transmitido desde un origen hacia un destino pudiendo pasar por varios [[Router|Routers]]. Cada uno de estos utiliza su *forwarding table* para reenviar los paquetes que recibe.

## Subnetting
#TODO
