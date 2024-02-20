La *CPU (Central Process Unit)* es el componente encargado de ejecutar las *instrucciones*.

La [[Arquitectura de Computadores#Arquitectura Von Neumann|Arquitectura Von Neumann]] propone que la misma cuente con los siguientes elementos:
- ALU (Arithmetic Logic Unit): [[Circuitos Combinatorios|Circuito Combinatorio]]\* que implementa operaciones de aritmética binaria y lógica.
- CU (Control Unit): [[Circuitos Secuenciales|Circuito Secuencial]] que implementa el [[#Ciclo de Instrucción]] en sincronización con el reloj del sistema. 
- [[#Set de Registros]]\*.

(\*) *Nótese: El [[#Set de Registros]] no es un elemento esencial de la [[Arquitectura de Computadores#Arquitectura Von Neumann|Arquitectura Von Neumann]].
(\*) *Nótese: Algunas ALU que implementan multiplicación y/o división suelen ser [[Circuitos Secuenciales]].*

## Ciclo de Instrucción
Secuencia de acciones que realiza la Unidad de Control para lograr ejecutar una instrucción del programa almacenado en memoria.

1. Fetch: Leer desde memoria la próxima instrucción a ejecutar. Conecta el [[Arquitectura de Computadores#Bus|Bus de Direcciones de Memoria]] con el registro PC, luego conecta el [[Arquitectura de Computadores#Bus|Bus de Datos de Memoria]] con el registro interno IR y coloca en el [[Arquitectura de Computadores#Bus|Bus de Control de Memoria]] las señales apropiadas para la realización de la lectura.
2. Decode: Decodificar el código binario de la instrucción para determinar operación, operandos y donde almacenar el resultado.
3. Read $(\star)$: Se accede a memoria para leer los operandos.
4. Execute: Ejecuta la operación por parte de la ALU.
5. Write $(\star)$: Almacena el resultado de la operación en el destino.
$(\star)$ Las operaciones *read* y *write* pueden ser opcionales en operaciones que no requieran leer operandos o que no requieran almacenar un resultado.

## Set de Instrucciones
Es el conjunto de instrucciones disponibles en el hardware del CPU. Se destacan dos filosofías diferentes:
- RISC (Reduced Instruction Set Computer): se cuenta con un *set de instrucciones* con instrucciones de *largo fijo* y *mínimas*.
- CISC (Complex Instruction Set Computer): se cuenta con un *set de instrucciones* con instrucciones de largo variable y *complejas*.

## Formato de Instrucciones
El *formato de las instrucciones* refiere a la codificación de las distintas instrucciones para su almacenamiento en la memoria del sistema.

Atributos que definen el formato de las instrucciones:
- Identificador
- Operandos a utilizar
- Largo de instrucción *(en caso de que el largo no sea fijo)*.

## Set de Registros
Conjunto de posiciones especiales de memoria *(registros)* que se encuentran dentro del CPU y mucho más veloces que si estuvieran en memoria.
- Totalmente Visibles: son manipulados *directamente* por el programador *(ej. AX, BX, AL).*
- Parcialmente Visibles: son manipulados *indirectamente* por el programador *(ej. IP (Instruction Pointer)[^IP], SP (Stack Pointer), FLAGS[^PS]).*
- Internos: son utilizados *exclusivamente* por el *Control Unit* *(ej. IR (Instruction Register)[^IR])*.

[^IP]: También conocido como *PC (Program Counter)*. Contiene la próxima instrucción a ejecutar.
[^PS]: También conocido como *PS (Process Status)*. Contiene las flags de *Overflow, Sign, Zero, etc.*
[^IR]: Contiene la instrucción que se el *Control Unit* decodificó.
## Modos de Direccionamiento
Los *modos de direccionamiento* establecen las formas en que se puede, a nivel de las instrucciones, especificar la dirección de un operando o del lugar donde colocar el resultado de la operación correspondiente a la instrucción.
- Inmediato: El argumento es el mismo operando.
- Directo: El argumento es una *referencia* al lugar donde se encuentra el operando.
	- Directo a Registro: La *referencia* es un registro.
	- Directo a Memoria: La *referencia* es una dirección de memoria.
- Indirecto: El argumento es una *referencia* al lugar donde se encuentra la dirección en memoria del operando.
	- Indirecto a Registro: La *referencia* es un registro.
	- Indirecto a Memoria: La *referencia* es una dirección de memoria.

## Implementación de CU
Hay dos filosofías de diseño diferenciadas para el *Control Unit*:
- Lógica Cableada: propone que el *Control Unit* se realize mediante un [[Circuitos Secuenciales|Circuito Secuencial]], de esta forma, ganando velocidad. Sin embargo, esta filosofía cuenta con poca flexibilidad, pues cualquier cambio implicaría rediseñar el circuito.
- Lógica Micro-Programada: propone que cada instrucción se ejecute a partir de un *microprograma*, es decir, una secuencia de *microinstrucciones*. Por lo tanto, al modificar el [[#Set de Instrucciones]], no habrá necesidad de rediseñar el *Control Unit*. Sin embargo, disminuye la velocidad, ya que cada *microinstrucción* deberá ser leída del *microprograma* que estará almacenados en una [[Read-Only Memory|ROM]].
	- Horizontal: cada instrucción se representa como una secuencia de microinstrucciones.
	- Vertical: cada instrucción se divide en *campos de control*. Cada *campo de control* activa los componentes específicos del CPU para ejecutar una parte particular de la instrucción.