## Concepto de Archivo
Un *archivo (file)* es una secuencia de *registros*[^registro] que representa datos *(ej. imagen .png, audio .mp3, documento de texto .txt)* y es guardado en almacenamiento secundario. Representa la unidad de almacenamiento mínima en almacenamiento secundario.

[^registro]: El concepto de *registro* depende del tipo de archivo, por ejemplo, en un `.txt` el *registro* podría representar un código ASCII.

### Metadata
Los archivos poseen ciertos atributos denominados *metadata*. Entre ellos se destacan:
- Nombre
- Identificador
- Tipo
- Ubicación
- Tamaño
- Protección/Permisos
- Información de conteo *(fecha creación, último acceso, etc)*.

### Operaciones sobre Archivos
El [[Sistema Operativo]] provee [[Sistema Operativo#System Calls|System Calls]] para la manipulación de archivos:
- Creación de archivos.
- Escritura de archivos.
- Lectura de archivos.
- Reposicionamiento dentro de un archivo.
- Eliminación de archivos.
- Truncamiento de un archivo, es decir, eliminar los datos de un archivo pero manteniendo su metadata.

### Estructura Interna
Por lo general, los dispositivos de almacenamiento secundario definen el tamaño de la unidad *block* que determinado por el tamaño de un sector, pues un *block* abarcará uno o más sectores *(ej. 1 block = 512 bytes)*. Por ende, todas las operaciones I/O se realizan en unidades *block*.

>[!warning] 
>Al tener un tamaño *block* fijo, en la mayoría de los casos los archivos desperdician los últimos bits de su último *block*.

### Métodos de Acceso
- Acceso Secuencial: La información es accedida de manera secuencial, *registro* a *registro*.[^registro] *El SO provee las operaciones `.txt` & `read_next()` sobre los archivos.*
- Acceso Directo: El archivo se presenta como una secuencia numerada de registros. De esta forma, la información puede ser accedida en cualquier orden, pues no existen restricciones sobre el orden de lectura/escritura. *El SO provee las operaciones `write_next()` & `read(n)` donde `write(n)` es un índice asociado al block del que se quiere leer/escribir*.

## Open-File Table
El [[Sistema Operativo]] mantiene una tabla llamada *open-file table* que almacena cierta información sobre los archivos en uso dentro del sistema.

## Directorios
Un *directorio* es una tabla que asocia *file names* con su respectivo *directory entry*.

### Operaciones
El [[Sistema Operativo]] provee [[Sistema Operativo#System Calls|System Calls]] para la manipulación de directorios:
- Búsqueda de archivos.
- Crear archivos.
- Eliminar archivos.
- Listar archivos.
- Renombrar archivos.
- Permitir navegación sobre el *file system*.

### Estructura de Directorios
- Nivel Único: Todos los archivos del *file system* se encuentran en un mismo directorio.
- Dos Niveles: Existen dos niveles de directorios.
- Árbol: El sistema ve los directorios como archivos, lo que permite al usuario tener *sub-directorios*. Además, surgen los siguientes términos:
	- *Absolute path name*: Empieza en la raíz del árbol y termina en un archivo especifico *(ej. root/home/work/todo.txt)*.
	- *Relative path name*: Empieza en un directorio especifico y termina en un archivo especifico *(ej. work/todo.txt)*.
- Grafo: A diferencia de la *estructura árbol*, la *estructura grafo* permite compartir archivos entre distintos directorios mediante *links*.
	- Soft Link: Referencia a un archivo en diferentes directorios.
	- Hard Link: Duplica la información de un archivo en diferentes directorios.

### Implementación
- Linear List: Se implementa una lista donde cada nodo representa el nombre de un archivo perteneciente al directorio y una referencia a su *directory entry*.
- Hash Table: Con el nombre de los archivos se genera un *hash* que identificará el bloque en el cual se encuentra su *directory entry*.

>[!warning] 
>Al crear un archivo se deberá verificar que el archivo no este exista dentro del directorio. Lo que conlleva recorrer el directorio en su totalidad en una implementación con *linear list*.

## Montaje
Un sistema puede poseer varios dispositivos de almacenamiento. Donde cada uno de ellos, puede ser dividido físicamente en una o varias *particiones*, donde cada *partición* funcionará como un dispositivo de almacenamiento independiente.

Un *volumen* es una entidad lógica, que abarca una o varias *particiones*, de esta forma, pudiendo combinar varios dispositivos de almacenamiento en un único espacio de almacenamiento lógico.

Luego, los volúmenes se formatean con un *file system* o son dejados *raw (sin formato)* por ejemplo, para ser usado como *swap space*.

## Seguridad
En un sistema multi-usuario, es necesario proteger la información de cada usuario. Para esto, se crean *grupos de usuario* según el uso que tendrán en el sistema. *(ej. Administradores, Estudiantes, Técnicos, etc).* A su vez, se definen permisos sobre los archivos según el usuario y/o grupos.

## Diseño
El *file system* se implementa en capas, donde cada capa utiliza una interfaz implementada por la capa inferior.
1. *application programs $\downarrow$* 
2. *logical file system $\downarrow$*
3. *file-organization module $\downarrow$*
4. *basic file system $\downarrow$*
5. *I/O control $\downarrow$*
6. *storage devices.*

Un *file system* básico, necesita emitir ciertos comandos genéricos hacia el dispositivo de almacenamiento para la lectura/escritura de *physical blocks*. Cada *physical block* es identificado por un número que hace referencia a su ubicación dentro del dispositivo *(ej. drive 1, cylinder 73, track 2, sector 10)*.

El *logical file system* se administra toda la *metadata* de del *file system* excepto de los datos de los archivos. Mantiene la estructura de los archivos mediante *file-control blocks*[^fcb].

[^fcb]: Un *file-control block (FCB)* contiene información sobre el archivo *(propietarios, permisos, ubicación de los datos)*.

>[!info] *inode* $\equiv$ *file-control block*
>En sistemas POSIX, se denomina *inode* a un *file-control block (FCB)*.

## Estructura en Hardware
Los *dispositivos de almacenamiento* contienen las siguientes estructuras:
- Boot Control Block *(por volumen)*: Necesario para iniciar el sistema operativo desde cierto volumen. Por lo general, este es el primer bloque del volumen y podría estar vacío en caso de no contener un SO.
- Volume Control Block *(por volumen)*: Contiene detalles del volumen *(ej. cantidad de bloques, tamaño del bloque, cantidad de bloques libres, referencias a bloques libres, cantidad de FCB[^fcb] libres, referencias a FCB[^fcb] libres).*
- Estructura de Directorio *(por file system)*: Usada para organizar los archivos.
- File-Control Block (FCB)[^fcb].

>[!example] *superblock* & *inodes*
>En sistemas Unix, por cada dispositivo de almacenamiento montado como un *file system* el kernel mantiene un *superblock*. Un *superblock* representa un *file system* y su principal función es proveer acceso a los *file-control blocks*[^fcb] *(conocidos como inodes en Unix)*.
>

## Estructura en Memoria
El sistema operativo mantiene en memoria las siguientes estructuras:
- Tabla de Montado: Contiene información sobre los volumenes montados.
- Caché con Estructura de Directorios: Información de los directorios accedidos recientemente.
- Una copia del FCB de cada archivo abierto.
- Punteros a la tabla global de archivos abiertos.

## Virtual File System
El sistema operativo implementa interfaces usando técnicas de *programación orientada a objetos* para simplificar y modularizar la implementación de diferentes *file systems*, de esta forma, implementar varios *file systems* en la misma estructura.

Para lograr esto, se diseña una estructura en tres capas:
1. *file system interface $\downarrow$*
2. *virtual file system (VFS) $\downarrow$*
3. *implementación especifica del file system (ej. FAT, NTFS, etc)*.

## Métodos de Asignación
- Contiguous Allocation: Los bloques asociados a un archivo son almacenados de manera contigua. Para su funcionamiento, se necesita una referencia al *bloque inicial* y la *cantidad de bloques*.
- Linked Allocation: Los bloques asociados a un archivo son almacenados de forma encadenada. Se necesita una referencia al *bloque inicial* y *bloque final*. Además, cada bloque tendrá una referencia al siguiente bloque.
- Indexed Allocation: Cada archivo tendrá su propio *index block* donde la *i-esima* entrada  de este apuntará al *i-esimo* bloque del archivo. Los directorios contendrán las referencias a los respectivos *index blocks* asociados a los archivos del mismo.
  Por otra parte, una asignación *indexed allocation* permite *copy-on-write*[^copy-on-write] de manera eficiente.

>[!important] 
>En sistemas POSIX, se utiliza una modificación de *Indexed Allocation*, donde además de que cada archivo pueda referenciar directamente cierta cantidad de bloques de datos, también permite referenciar indirectamente con las siguientes referencias:
>- Puntero de *Indirección Simple*: Apunta a un bloque que referencia bloques de datos del archivo.
>- Puntero de *Indirección Doble*: Apunta a un bloque que referencia bloques que referencian datos del archivo.
>- Puntero de *Indirección Triple*: Apunta a un bloque de referencia bloques que referencian  bloques que referencian bloques de datos del archivo.

[^copy-on-write]: Cuando se desea modificar un bloque en un *file system* de tipo *copy-on-write*, se escribe un nuevo bloque y se elimina el bloque anterior de forma atómica. De esta forma, permite solucionar problemas de inconsistencia, pues si surge un error al ejecutar la operación, el bloque anterior seguirá siendo valido.

## Administración de Espacio Libre
- Bit Map: Se dispone de un bit por cada bloque que representa si este está ocupado o libre.
- Linked List: Se mantiene una *linked list* de los bloques libres.
- Grouping: Es una variante de *linked list*, donde cada nodo contiene un grupo de bloques libres.
- Counting: Es una variante de *linked list*, donde cada nodo contiene un bloque y la cantidad de bloques contiguos libres existen después de este.

