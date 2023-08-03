La *CPU (Central Process Unit)* es el componente encargado de ejecutar las *instrucciones*.

La [[Arquitectura von Neumann]] propone que la misma cuente con los siguientes elementos:
- ALU (Arithmetic Logic Unit): Circuito lógico que implementa operaciones de aritmética binaria. *Casualmente implementa operaciones de desplazamiento y/o rotación de bits*.
- Unidad de Control (UC): [[Circuitos Secuenciales|Circuito Secuencial]] que implementa el [[#Ciclo de Instrucción]] en sincronización con el reloj del sistema. 
- Banco de Registros: Posiciones especiales de memoria *(registros)* mucho más veloces que si estuvieran en memoria.
	- Totalmente Visibles: Almacenan operandos y/o direcciones de memoria para ser usados en las instrucciones. Estos son manipulados *directamente* por el programador.
	- Parcialmente Visibles: Registros que tienen funcionalidades especiales, son manipulados *indirectamente* por el programador *(ej. IP (Instruction Pointer), PC (Program Counter), SP (Stack Pointer), PS (Process Status))*.
	- Internos: Registros utilizados por la *Unidad de Control* para la ejecución de instrucciones *(ej. registros A...F de uso exclusivo para la Unidad de Control)*. No son manipulables por el programado.

>[!info] 
>El *conjunto de registros* no es un elemento escencial de la [[Arquitectura von Neumann]].

Una arquitectura particular basada en la [[Arquitectura von Neumann]] establece en forma diferente ciertos elementos, que deben ser conocidos por el programador para poder escribir programas en una de estas arquitecturas.
- [[#Set de Registros]]
- [[#Set de Instrucciones]]
- [[#Formato de Instrucciones]]
- [[#Modos de Direccionamiento]]
- Manejo de [[Input & Output]]
- Manejo de [[Interrupciones]]

## Ciclo de Instrucción
Secuencia de acciones que realiza la Unidad de Control para lograr ejecutar una instrucción del programa almacenado en memoria.

1. Fetch: Leer desde memoria la próxima instrucción a ejecutar. Conecta el [[Arquitectura von Neumann#Bus|Bus de Direcciones de Memoria]] con el registro PC, luego conecta el [[Arquitectura von Neumann#Bus|Bus de Datos de Memoria]] con el registro interno IR y coloca en el [[Arquitectura von Neumann#Bus|Bus de Control de Memoria]] las señales apropiadas para la realización de la lectura.
2. Decode: Decodificar el código binario de la instrucción para determinar operación, operandos y donde almacenar el resultado.
3. Read $(\star)$: Se accede a memoria para leer los operandos.
4. Execute: Ejecuta la operación por parte de la ALU.
5. Write $(\star)$: Almacena el resultado de la operación en el destino.
$(\star)$ Las operaciones *read* y *write* pueden ser opcionales en operaciones que no requieran leer operandos o que no requieran almacenar un resultado.

## Set de Instrucciones
Es el conjunto de instrucciones disponibles en el hardware del CPU. Se destacan dos filosofías diferentes:
- RISC (Reduced Instruction Set Computer): El *set de instrucciones* es un conjunto mínimo donde sus operaciones están implementadas de forma eficiente. Además el largo de las instrucciones es de un fijo fijo.
- CISC (Complex Instruction Set Computer): Se cuenta con un *set de instrucciones* donde el largo de estas pueden variar.

## Formato de Instrucciones
El *formato de las instrucciones* refiere a la codificación de las distintas instrucciones para su almacenamiento en la memoria del sistema.

Atributos que definen el formato de las instrucciones:
- Identificador
- Operandos a utilizar
- Largo de instrucción *(en caso de que el largo no sea fijo)*.

## Set de Registros
Conjunto de posiciones especiales de memoria *(registros)* que se encuentran dentro del CPU y mucho más veloces que si estuvieran en memoria. *Algunos de estos registros son utilizados únicamente por la CPU*.

## Modos de Direccionamiento
Los *modos de direccionamiento* establecen las formas en que se puede, a nivel de las instrucciones, especificar la dirección de un operando o del lugar donde colocar el resultado de la operación correspondiente a la instrucción.
- Inmediato: El argumento es el mismo operando.
- Directo: El argumento es una *referencia* al lugar donde se encuentra el operando.
	- Directo a Registro: La *referencia* es un registro.
	- Directo a Memoria: La *referencia* es una dirección de memoria.
- Indirecto: El argumento es una *referencia* al lugar donde se encuentra la dirección en memoria del operando.
	- Indirecto a Registro (indizado): La *referencia* es un registro.
	- Indirecto a Memoria: La *referencia* es una dirección de memoria.

## Lógica
Hay dos filosofías de diseño diferenciadas para la Unidad de Control:
- Cableada: Propone que la *Unidad de Control* se realize mediante un [[Circuitos Secuenciales|Circuito Secuencial]], de esta forma, ganando velocidad. Sin embargo, esta filosofía cuenta con poca flexibilidad, pues cualquier cambio implicaría rediseñar el circuito.
- Microprogrammed: Propone que el [[#Ciclo de Instrucción]] se ejecute siguiendo un *microprogram*[^2] que contienen los valores de las señales apropiadas para dicha instrucción, de esta forma, al modificar el [[#Set de Instrucciones]], no habrá necesidad de rediseñar la *Unidad de Control*. Sin embargo, disminuye la velocidad, ya que los *microprograms*[^2] se encuentran dentro de una [[Read-Only Memory|ROM]].
 
## Microprogramming
Es una técnica utilizada en el diseño de *microprocesadores* para implementar instrucciones de máquina. Existen dos enfoques principales:
- Horizontal: Cada instrucción se representa como una secuencia de microinstrucciones.
- Vertical: Cada instrucción se divide en *campos de control*. Cada *campo de control* activa los componentes específicos del CPU para ejecutar una parte particular de la instrucción.

## Banco de Registros
#TODO

[^1]: Una *microinstruction* contiene señales de control que activan los diferentes componentes del procesador para ejecutar la instrucción correspondiente.
[^2]: Un *microprogram* es una secuencia de *microinstructions*.[^microinstruction]
