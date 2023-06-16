***
## Segment
Un *chunk* de memoria asignado a un proceso.
***
## Physical Address
Una *physical address* es una *memory address* real dentro de la memoria física.
***
## Asignación de Address Space
La asociación de instrucciones y datos de dirección de memoria se pueden realizar en las siguientes etapas:
- Compile Time: El proceso se asigna a un lugar especifico de la memoria física, empezando desde una *posición inicial* $k$.
- Load Time: Durante *compile time*, no se sabe donde vivirá el proceso en la memoria. Por ende, el compilador deberá generar direcciones reubicables. Una vez que el proceso se carga, el SO determina la *posición inicial* $k$ del proceso dentro de la memoria física.
- Execution Time: Un proceso puede variar su posición en memoria durante su ejecución. Por lo tanto, el compilador deberá generar direcciones reubicables, de esta forma, el SO se encargará de determinar la posición del proceso en memoria física mientras este se ejecuta.

## Estrategias de Asignación
- First Fit: Asigna el primer fragmento de memoria disponible.
- Best Fit: Asigna el fragmento de memoria disponible que minimize la memoria disponible luego de dicha asignación.
- Worst Fit: Asigna el fragmento que posee mayor memoria disponible.
