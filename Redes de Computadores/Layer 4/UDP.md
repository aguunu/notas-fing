El [[Protocolo]] UDP (User Datagram Protocol), no garantiza la confianza al transferir datos entre procesos, en pocas palabras, el protocolo UDP ni siquiera garantiza que el mensaje vaya a llegar a su destino, e incluso los mensajes pueden llegar desordenados. 

>[!quote] 
>El protocolo UDP se basa en enviar un segmento a la [[Capa de Red]] y que salga lo que dios quiera.

*Nota: en el protocolo UDP no existe un handshake entre el host origen y destino, esto es, no existe una conexión entre el origen y destino, logrando que el UDP sea "connectionless".*

![[Drawing 2024-01-30 15.46.34.excalidraw]]

Se hace uso de [[Detección y Corrección de Errores#Checksum|Checksum]] para la detección de errores en los segmentos UDP transmitidos.

>[!attention] 
>A pesar de que UDP no garantiza confianza en la transferencia de datos, los protocolos de capas superiores pueden implementar sus propios mecanismos para la transferencia de datos confiable como es el caso de [[DNS]].
