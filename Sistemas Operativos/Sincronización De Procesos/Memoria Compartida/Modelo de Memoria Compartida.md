En un *modelo de memoria compartida*, los procesos que se comunican establecen un segmento de memoria compartida. Luego, los procesos podrán intercambiar información leyendo y escribiendo datos sobre el segmento de memoria compartida. Típicamente, este segmento reside en el *address space* del proceso que crea la comunicación. 

Los procesos que deseen comunicarse, deberán agregar dicho segmento en sus correspondiente *address space*.

>[!bug] Datos Inconsistentes
>El acceso concurrente entre varios procesos a datos compartidos puede resultar en *datos inconsistentes.*
