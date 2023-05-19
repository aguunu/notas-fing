El *modelo de pasaje de mensajes* provee un mecanismo que permite al proceso comunicarse y sincronizar sus acciones sin compartir el mismo *address space*.

>[!important]
>El *modelo de pasaje de mensajes* es particularmente útil en ambientes distribuidos, donde los procesos que se comunican residen en diferentes computadoras conectadas a través de una red.

## Send && Receive
Se proveen dos operaciones `send(message)` y `receive(message)`, el mensaje enviado por un proceso puede ser de tamaño fijo o variable. Además, el *kernel* funciona como intermediario entre el proceso emisor y el proceso receptor.

## Comunicación
Si dos procesos `P` y `Q` desean comunicarse, debe existir un *vinculo de comunicación* entre ellos. El funcionamiento de este *vinculo* depende de la implementación lógica de las funciones `send` y `receive`.

### Comunicación Directa e Indirecta
Los procesos que desean comunicarse deben tener una forma de referenciarse entre ellos.

#### Comunicación Directa
Cada proceso que desea comunicarse debe referenciar explícitamente al receptor/emisor del mensaje.
- `send(P, message)`: Emite un mensaje al proceso `P`.
- `receive(Q, message)`: Recibe un mensaje del proceso `Q`.

La cardinalidad de este método es $N \times 1$, pues existen múltiples emisores y un único receptor.

#### Comunicación Indirecta
Los mensajes son recibidos y emitidos a través de *mailboxes*.
- `send(M, message)`: Emite un mensaje al *mailbox* `M`.
- `receive(M, message)`: Recibe un mensaje del *mailbox* `M`.

La cardinalidad de este método es $N \times M$, pues existen múltiples emisores y múltiples receptores.

>[!warning] 
>Si un proceso $p_1$ emite un mensaje al *mailbox* `M`, mientras que los procesos $p_2$ y $p_3$ ejecutan `receive(M)`, el proceso que reciba el mensaje enviado por $p_1$ dependerá de la lógica de la implementación.
>

### Comunicación Sincrónica y Asincrónica
La comunicación entre procesos puede ser *blocking* o *nonblocking*, también conocido como *synchronous* y *asynchronous*.

- **Blocking Send**: El emisor se bloquea hasta que el mensaje sea recibido por el receptor o mailbox.
- **Nonblocking Send**: El emisor emite el mensaje y continua con su ejecución.
- **Blocking Receive**: El receptor se bloquea hasta que un mensaje este disponible.
- **Nonblocking Receive**: El receptor recibe un mensaje valido o `NULL`.

### Buffering
Si la comunicación es *directa* o *indirecta*, los mensajes intercambiados por los procesos residen en una *queue* temporal. Esta *queue* pude implementarse de las siguientes maneras:
- **Capacidad Finita**: La *queue* tiene una capacidad $n$, por lo tanto, podrán haber a lo sumo $n$ mensajes dentro de ella. Si la *queue* llega a su capacidad máxima, el emisor se bloqueará hasta que halla lugar disponible. *Este caso también abarca una queue con capacidad $0$*.
- **Capacidad Infinita**: La capacidad de la *queue* es infinita. Por lo tanto, el emisor nunca se bloquea.
