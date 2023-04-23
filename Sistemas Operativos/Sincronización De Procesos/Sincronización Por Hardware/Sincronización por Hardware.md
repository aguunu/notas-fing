El [[Sección Crítica#Problema de la Sección Crítica|Problema de la Sección Crítica]] puede ser resuelto fácilmente en un sistema *single-processor* si pudiéramos deshabilitar las [[Interrupciones]] mientras la variable compartida esta siendo modificada. Sin embargo, en un sistema *multi-processor* esta solución consumiría mucho tiempo (el mensaje se pasaría a todos los procesadores).
A pesar de esto, los sistemas modernos proveen instrucciones de hardware atómicas para resolver este problema.

>[!abstract] 
>Las soluciones eficientes para el [[Sección Crítica|Problema de la Sección Crítica]] requieren asistencia del hardware y del sistema operativo. Además, todas estas soluciones se basan en *locking*, encargándose de proteger la [[Sección Crítica]] a través de *locks*.
