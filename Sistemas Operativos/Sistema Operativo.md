El *sistema operativo (SO)* es un programa que funciona como una interfaz entre el usuario y el hardware, escondiendo así detalles sobre la arquitectura en la que se esta trabajando.

## Objetivos
Los sistemas operativos tienen diferentes objetivos dependiendo su fin, por ejemplo, los sistemas operativos para servidores se destacan por la optimización del hardware. En cambio, sistemas operativos usados en smartphones proveen una interfaz para que el usuario pueda interactuar fácilmente con el software.
Por ende, algunos sistemas están centrados en la *eficiencia* y otros en la *conveniencia* del mismo.

## Componentes Principales
- [[Scheduling|Planificación de Procesos]]
- [[Administración de Memoria]]
- [[File System]]
- [[Input & Output System]]

## System Services
Un sistema operativo brindará servicios que serán accesibles para el usuario mediante una interfaz definida.

Se brinda un conjunto de servicios con la finalidad de ayudar al usuario del SO, entre ellos se destacan:
- Interfaz de usuario
- Ejecución de programas
- Operaciones I/O
- Manipulación del [[File System]]
- Comunicaciones
- Detección de errores

Existe otro conjunto de servicios que proveen funcionalidades que no ayudan al usuario pero aseguran la eficiencia del sistema operativo:
- Administración de recursos
- Conteo de recursos
- Protección y seguridad

## Protección del Hardware
El hardware suministra al sistema operativo mecanismos para la protección, entre ellos se destacan:
- **Dual Mode**: El hardware provee distintos modos de ejecución, de los cuales se destacan:
	1. *User Mode*: Únicamente se podrá ejecutar un conjunto reducido de instrucciones de hardware.
	2. *Kernel Mode (Monitor)*: Todas las instrucciones del hardware están disponibles. Sin embargo, el sistema operativo es el único que debe ejecutar este modo, por esta razón, el SO provee *system calls* para el uso de estas instrucciones privilegiadas.
- **Protección I/O**: Todas las instrucciones de entrada y salida son [[#Instrucciones Privilegiadas|Privilegiadas]]. 
- **Protección de Memoria**: Traducir las direcciones de memoria a través de la [[Memory Management Unity|MMU]].
- **Protección de CPU**: Introducción de un *timer* que limita el uso del CPU a los procesos.

## System Calls
Un *system call* es una interfaz, provista por el *kernel*, para que los [[Procesos]] accedan a los diferentes servicios que brinda el sistema operativo.

El proceso de realizar una *system call* generalmente implica los siguientes pasos:
1. Cargar los argumentos (parámetros) en el stack y/o registros del CPU.
2. Cargar el identificador del *system call* en un registro especifico correspondiente a la arquitectura *(rax en x86)*.
4. Invocar el *system call handler* adecuado.
5. El procesador pasa a *kernel mode* a través de una [[#Excepción|Trap]].
6. El *kernel* ejecuta la *system call* y retorna el resultado en un registro especifico correspondiente a la arquitectura *(rax en x86)*.
7. El procesador vuelve a *user mode* a través de una [[#Excepción|Trap]].
8. Se otorga el control del CPU al proceso que invocó el *system call*.

Podemos clasificarlos de la siguiente manera:
- Control de procesos
- Gestión de archivos
- Gestión de dispositivos
- Gestión de información del sistema
- Comunicaciones

## Diseño de un Sistema Operativo
### Sistema Monolítico
Los *sistemas monolíticos* implementan en el kernel los componentes fundamentales del sistema operativo.

### Sistema por Capas
En un *sistema por capas*, se busca organizar el diseño del sistema operativo en una jerarquía de capas construidas una encima de la otra. Los servicios que provee cada capa son consumidos únicamente por capas que se encuentren en un nivel superior.

### Sistema Microkernel
Se busca que el kernel sea lo más pequeño posible, limitándose a proporcionar los servicios básicos de un SO. 

***

## Excepción
Una *excepción* o también conocido como *trap* es una interrupción generada a nivel de software invocada por un error o por un solicitud de un usuario a un servicio especifico del sistema operativo.

## Instrucciones Privilegiadas 
Son aquellas instrucciones que únicamente se pueden ejecutar en *kernel mode* ya que pueden potencialmente dañar otros procesos *(ej. operaciones de I/O, actualizar el clock, desactivar interrupciones, manipular el [[Memory Management Unity|MMU]], manipular el bit del Dual Mode, etc)*.
