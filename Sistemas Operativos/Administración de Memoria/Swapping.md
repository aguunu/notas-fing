La técnica de *swapping* permite que el [[Administración de Memoria#Address Space|Address Space]] de los procesos exceda con respecto al limite del [[Administración de Memoria#Physical Address Space|Physical Address Space]] del sistema. Aumentando, de esta forma, el [[Scheduling#Grado de Multiprogramación|Grado de Multiprogramación]].

## Backing Store
Lugar en memoria secundaria dónde se dispondrá un conjunto procesos.

Al mecanismo de llevar un proceso de memoria principal a memoria secundaria se le denomina *swap-out*, análogamente, *swap-in*.

>[!warning] 
>El tiempo de transferencia al hacer un *swap-in/swap-out* es extremadamente alto para el CPU.



