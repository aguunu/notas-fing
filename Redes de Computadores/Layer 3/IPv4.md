
![[Drawing 2024-01-28 16.40.28.excalidraw|center]]

## IPv4 Address
Una *IPv4 address* es un dirección de 32 bits que pertenece a uno de los siguientes grupos:
- *unicast*
- *multicast*
- *broadcast*

Además, existen ciertos bloques para direccionamiento privado:
- Clase A Privada `10.0.0.0/8`
- Class B Privada: `172.16.0.0/12`
- Class C Privada: `192.168.0.0/16`

>[!hint] 
>Por lo general, la primer dirección de una red se reserva para la identificación de esta, mientras que la última se reserva para la dirección de broadcast.

## Fragmentación
Cada nodo de la red chequea si el tamaño de cada paquete IP que intenta enviar es soportado por el [[Maximum Transmission Unit|MTU]] del próximo nodo. En caso de que un paquete IP exceda el [[Maximum Transmission Unit|MTU]] del próximo nodo, este es dividido en fragmentos, reensamblándose únicamente cuando todos los fragmentos llegan al destino final. 

IPv4 presenta información sobre la fragmentación en el *header*:
- $\texttt{Fragment Offset}$: indica el desplazamiento del primer byte del fragmento respecto al primer byte del datagrama IP. ==Este campo se mide en unidades de 8 bytes==.
- $\texttt{MF}$ (*flag - more fragments*): indicando que hay más fragmentos (esta encendida en todos los fragmentos excepto por el último)
- $\texttt{DF}$ (*flag - do not fragmentate*): indica que el paquete no podrá ser fragmentado.
*Notar: cada fragmento posee el mismo valor en el campo $\texttt{identification}$*.


>[!example] 
>Se enviará el datagrama [[IPv4]] `[lenght=4000|id=x|fragflag=0|offset=0|...]` por un enlace cuyo [[Maximum Transmission Unit|MTU]] es de 1.500 bytes.
>En primer lugar, asumiendo que el tamaño de la cabecera [[IPv4]] es de 20 bytes, obtenemos una carga útil de 1.500 bytes - 20 bytes = 1.480 bytes. Por ende, el datagrama original será fragmentado en los siguientes fragmentos:
>1. `[lenght=1500|id=x|fragflag=1|offset=0|...]`
>2. `[lenght=1500|id=x|fragflag=1|offset=185|...]`
>3. `[lenght=1040|id=x|fragflag=0|offset=370|...]`

