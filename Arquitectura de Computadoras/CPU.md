La CPU esta conformada por tres componentes fundamentales:
- ALU *Arithmetic logic unity*: Es un circuito lógico que implementa operaciones de aritmética binaria.
- CU *Control Unity*:  Es un circuito secuencial que implementa el ciclo de instrucción.
- Banco de Registros: Serie de posiciones especiales en memoria de la CPU, permiten el acceso a operandos y lugares de almacenamiento.

## Banco de Registros
Contiene registros que se dividen en ciertas categorías.

### Totalmente Visibles
Son los registros que contienen operandos o direcciones para su utilización en las instrucciones.

### Parcialmente Visibles
Son los registros que tienen funciones especiales pero participan de algún modo indirecto con las instrucciones.
- IP/PC
- SP
- PS/Registro de FLAGS

### Internos
Son los registros que utiliza la *Unidad de Control* para poder ejecutar las instrucciones.

## Ciclo de Instrucción
- Fetch: Lee desde la memoria la próxima instrucción a ejecutar.
- Decode: Se decodifica de la instrucción.
- Read (Opcional): Se accede a memoria para leer los operandos necesarios.
- Execute: Ejecuta la instrucción.
- Write (Opcional): Se escribe el resultado en el destino indicado por la instrucción.

## Lógica Cableada vs Micro-Programada
En la lógica cableada, la lógica se encuentra implementada en un circuito. Mientras que en la lógica micro-programada el usuario se encarga de la implementación.
Además, la lógica cableada es más eficiente que la micro-programada. Sin embargo, también es más costosa.




