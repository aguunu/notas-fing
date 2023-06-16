Técnica que permite a los procesos utilizar más memoria de la que está físicamente disponible en el sistema, proporcionando una abstracción adicional llamada *virtual address space*.

## Virtual Address Space
Rango completo que contiene todas las *virtual address* disponibles para cierto proceso.

>[!success] 
>Cada proceso contará con su propio *virtual address space*. Por lo tanto, un proceso no podrá acceder a una *virtual address space* de otro.

### Virtual Address
Una *virtual address* es una clase *memory address* utilizada por un proceso dentro de su *virtual address space* que se corresponde (indirectamente) una *physical memory address*.