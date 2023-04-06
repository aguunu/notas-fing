La E/S es una interfaz entre los programas que ejecuta la CPU y sus periféricos. Esto permite introducir la información a procesar en el sistema (entrada), y por otro lado presentar el resultado de dicho proceso (salida).

## Bus
Conexión entre la CPU, la memoria, y E/S, se realiza mediante un grupo de líneas (bus) que comunican: dirección, datos y control.

### Buses de Dirección
Transporta las direcciones de memoria o E/S a ser accedidas durante la transferencia.

### Bus de Datos
Es el encargado de hacer el traspaso de información entre los sub-sistemas.

### Bus de Control
Transportan señales que controlan el uso del bus y la comunicación sobre el mismo.

### Clasificación
#### Bus Simple
Utiliza la filosofía "Master/Slave". El *Master* controla el uso del bus en todo momento. Mientras que el *Slave* debe esperar a ser habilitado por el *Master*.

#### Bus Inteligente
Cualquier entidad conectada tiene la capacidad de convertirse en *Master* del bus.
Cuando varias entidades requieren hacer uso del bus, se utiliza un método del *Arbitraje*.

##### Arbitraje Centralizado
Existe una entidad que tiene mayor jerarquía que las demás.

##### Arbitraje Distribuido
Todas las entidades conectadas tienen la misma jerarquía.

*Observación: existen otras clasificaciones discutibles.*

## Controlador de E/S
Un controlador de E/S contiene la inteligencia del periférico, por este motivo, el periférico es controlado por su controlador.