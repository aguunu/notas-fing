La sección crítica es una sección de código donde múltiples [[Procesos]] intentan acceder a un recurso compartido o realizar una tarea crítica al mismo tiempo.

## Problema de la Sección Crítica
Cuando varios procesos intentan acceder simultáneamente a un recurso compartido, pueden ocurrir problemas como *race conditions*, en los que el resultado final del programa depende del orden en que los procesos acceden al recurso compartido.

Para resolver este problema, se busca diseñar un protocolo que los procesos utilicen para cooperar entre ellos, y que a su vez cumplan con las siguientes condiciones:
1. **Exclusión Mutua**: Si un proceso esta ejecutando su sección crítica, ningún otro proceso podrá estar ejecutando en dicha sección crítica. ^8f593f
2. **Progreso**: Si varios procesos desean entrar a una sección crítica y esta se libera, la misma deberá ser asignada a uno de estos procesos. (Evita [[#Deadlock]]).
3. **Espera Acotada**: Existe un limite en la cantidad de veces que un proceso es permitido entrar en su sección crítica después de que otro proceso realizó una petición para entrar a su sección crítica. (Evita espera indefinida).

>[!important] Importante
>El *Problema de Sección Crítica* se puede generalizar para ser aplicado tanto a [[Procesos]] como a [[Threads]].

***
### Busy Waiting
Desperdicia ciclos del CPU que podrían ser aprovechados por otro proceso.

```c
// busy waiting
while (condicion); // no hacer nada
```

### Deadlock
Dos o más procesos están esperando indefinidamente por un evento que puede ser causado únicamente por alguno de estos procesos.
