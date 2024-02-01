Una solución al problema de performance del modelo [[Stop and Wait Protocols|Stop and Wait]] es el *pipelining*. Para esto es necesario definir una ventana de transmisión que definirá cuantos paquetes se pueden transmitir “simultáneamente” sin haber recibido un ACK.

## Go-Back-N

<iframe style="border-radius: 15px; background: #FFFFFFAA; height: 100vh; width: 100%;" src=https://computerscience.unicam.it/marcantoni/reti/applet/GoBackProtocol/goback.html></iframe>

>[!warning] 
>Observar que si la capacidad de la ventana del emisor en *go-back n* es de tamaño $N$, entonces el espacio de números de secuencia deberá tener un tamaño de al menos $N + 1$. En otro caso, podría ocurrir comportamiento inesperado.
## Selective Repeat

<iframe style="border-radius: 10px; background: #FFFFFFAA; height: 100vh; width: 100%;" src=https://computerscience.unicam.it/marcantoni/reti/applet/SelectiveRepeatProtocol/selRepProt.html></iframe>

>[!warning] 
>Observar que si la capacidad de la ventana en *selective repeat* es de tamaño $N$, entonces el espacio de números de secuencia deberá tener un tamaño de al menos $2N$. En otro caso, podría ocurrir comportamiento inesperado.