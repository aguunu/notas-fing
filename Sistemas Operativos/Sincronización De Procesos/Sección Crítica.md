La sección crítica es una sección de código donde múltiples [[Procesos]] intentan acceder a un recurso compartido o realizar una tarea crítica al mismo tiempo.

## Problema de la Sección Crítica
Cuando varios procesos intentan acceder simultáneamente a un recurso compartido, pueden ocurrir problemas como *race conditions*, en los que el resultado final del programa depende del orden en que los procesos acceden al recurso compartido.

Para resolver este problema, se busca diseñar un protocolo que los procesos utilicen para cooperar entre ellos, y que a su vez cumplan con las siguientes condiciones:
1. **Exclusión Mutua**: Si un proceso esta ejecutando su sección crítica, ningún otro proceso podrá estar ejecutando en su sección crítica. ^8f593f
2. **Progreso**: Si varios procesos desean entrar a una sección crítica y esta se libera, la misma deberá ser asignada a uno de estos procesos. (Evita [[#Deadlock]]).
3. **Espera Acotada**: Si un proceso $p$ solicita ingresar a su sección crítica, debe haber un límite en el número de veces que otros procesos entran en su respectiva sección crítica, antes de que $p$ lo haga. (Evita *espera indefinida*).

>[!important] Importante
>El *Problema de Sección Crítica* se puede generalizar para ser aplicado tanto a [[Procesos]] como a [[Threads]].

***
### Busy Waiting
El *busy waiting (espera activa)* es una forma de esperar por un determinado evento, haciendo uso de un bucle que su único funcionamiento es desperdiciar ciclos del CPU.

```c
// busy waiting
while (condicion); // no hacer nada
```

>[!bug] Ciclos del CPU
>Los ciclos del CPU desperdiciados por *busy waiting* podrían ser aprovechados por otro proceso.

### Deadlock
Dos o más procesos están esperando indefinidamente por un evento que puede ser causado únicamente por alguno de estos procesos.
