***
## Segment
Un *chunk* de memoria asignado a un proceso.
***
## Address Space
El rango de memoria que puede ser referenciada es llama *address space*.

## Physical Address Space
El rango de memoria física que puede ser referenciada es llama *physical address space*.

### Physical Address
Una *physical address* es una *memory address* real dentro de la memoria física.
***
## Address Binding
Los métodos de asociación de direcciones, se refieren a cómo se realiza la asignación de [[Virtual Memory#Virtual Address|Virtual Address]] a [[#Physical Address]] en un sistema informático.

- Compile Time: El proceso se asigna a un lugar especifico de la memoria física, empezando desde una *posición inicial* $k$.
- Load Time: Durante *compile time*, no se sabe donde vivirá el proceso en la memoria. Por ende, el compilador deberá generar direcciones reubicables. Una vez que el proceso se carga, el SO determina la *posición inicial* $k$ del proceso dentro de la memoria física.
- Execution Time: Un proceso puede variar su posición en memoria durante su ejecución. Por lo tanto, el compilador deberá generar direcciones reubicables, de esta forma, el SO se encargará de determinar la posición del proceso en memoria física mientras este se ejecuta.

## Estrategias de Asignación
- First Fit: Asigna el primer fragmento de memoria disponible.
- Best Fit: Asigna el fragmento de memoria disponible que minimize la memoria disponible luego de dicha asignación.
- Worst Fit: Asigna el fragmento que posee mayor memoria disponible.

## Dynamic Linking
Al ejecutar un programa, el sistema operativo localiza la librería externa. Si ocurren cambios sobre esta librería, el programa no necesitará ser re-compilado y lanzado como un nuevo ejecutable.

## Static Linking
Es la practica de copiar todas las librerías que el programa necesite dentro del ejecutable final. Este proceso es realizado por un *linker* al finalizar el proceso de compilación.