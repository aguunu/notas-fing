## Componentes
TODO

## System Services
TODO

## System Calls
Son una interfaz, provista por el *kernel*, para que los [[Procesos]] accedan a los diferentes servicios que brinda el sistema operativo.

El proceso de realizar una system call generalmente implica los siguientes pasos:
1. Cargar los argumentos (parámetros) en el stack, registros del CPU y/o bloque de memoria (apuntado a través de un registro).
2. Cargar el identificado del *system call* en un registro especifico correspondiente a la arquitectura (**rax** en x86).
3. Invocar el *system call handler* adecuado (interrupción por software *"trap"*).
4. El procesador pasa a *modo kernel*, luego el kernel identifica la *system call* y procesa los argumentos.
5. El *kernel* realiza las operaciones de la *system call* y retorna el resultado en un registro especifico correspondiente a la arquitectura (**rax** en x86).
7. El procesador vuelve a *modo usuario* y se retorna el control al proceso que invocó el *system call*.

Podemos clasificarlos de la siguiente manera:
- Control de procesos
- Gestión de archivos
- Gestión de dispositivos
- Gestión de información del sistema
- Comunicaciones

## Estructura
TODO

### Sistema Monolítico
TODO

### Sistema en Capas
TODO

### Sistema Microkernel
TODO

## Virtual Machine (VM)
TODO