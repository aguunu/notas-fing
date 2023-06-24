La técnica de *RAID (Redundant Array of Independent Disks)* brinda confiabilidad a través de información redundante, y/o performance a través de la disposición de la información en varios discos.
- *La redundancia surge al duplicar discos o a través de bits para control de errores*.
- *La performance surge por la lectura/escritura de forma paralela en varios discos gracias a la técnica de data striping[^striping] o bit-striping[^bit-striping].* 

[^striping]: La técnica de *data striping* consiste en dividir la información en varios segmentos de bits. 
[^bit-striping]: La técnica de *bit-striping* es un caso particular de *striping*[^striping]. Donde la información se divide en tantos segmentos como bits tenga.

## Niveles de RAID
- RAID 0, *non-redundant striping*
- RAID 1, *mirrored disks*
- RAID 2, *memory-style error-correcting codes*
- RAID 3, *bit-interleaved parity*
- RAID 4, *block-interleaved parity*
- RAID 5, *block-interleaved distributed parity*
- RAID 6, *P + Q redundancy*

>[!success] 
>Los [[#Niveles de RAID]] pueden ser combinados, en un RAID $i+j$, se aplica la técnica de RAID $j$ sobre un RAID $i$.

