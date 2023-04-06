## Lock Binario
Se consideran dos operaciones nuevas en una transacción $T_i$:
- $l_i(x)$ *lock*
- $u_i(x)$ *unlock*

Cuando se ejecuta $l_i(x)$, el DBMS hace que cualquier $l_j(x)$ de cualquier otra transacción $T_j$ no termine hasta que $T_i$ ejecute $u_i(x)$.

### Reglas de Uso
- Antes de que $T_i$ ejecute $r_i(x)$ o $w_i(x)$ debe ejecutar $l_i(x)$.
- Nunca se ejecuta $l_i(x)$ si este ya esta bloqueado.

### Características:
- Fácil de implementar
- Niega incluso la lectura a otras transacciones, cuando esto no es necesario.

## Read/Write Lock
Se consideran tres operaciones nuevas en una transacción $T_i$:
- $rl_i(x)$ *read lock*
- $wl_i(x)$ *write lock*
- $u_i(x)$ *unlock*

### Reglas de Uso
- Antes que $T_i$ ejecute $r_i(x)$, debe ejecutar $lr_i(x)$ o $wl_i(x)$ y luego de $r_i(x)$ debe ejecutar $u_i(x)$.
- Nunca se ejecuta un *read lock* o *write lock* sobre un ítem si este ya tiene ese mismo lock.
- Los *locks* se pueden promover o degradar.

### Características
- Permite que varias transacciones hagan *read lock* simultáneamente sobre el mismo ítem.
- Más difícil de implementar que **Lock Binario**.

## Protocolos de Locking
Un protocolo de locking define un conjunto de reglas de uso de *locks* que sean más fuertes que los anteriores y que garanticen seriabilidad.
*Observación: Para que una historia sea seriabilizable por 2PL, cada transacción de dicha historia debe cumplir con el protocolo 2PL.*

### Protocolo 2PL
Hay dos fases en una transacción:
1. Fase de crecimiento: Se crean *locks*
2. Fase de contracción: Se liberan *locks*

##### Básico
Solo exige las dos fases del protocolo 2PL.
- Susceptible a Deadlock

##### Conservador
Exige que todos los locks se hagan antes del comienzo de la transacción.
- No susceptible a Deadlock
- Exige la pre-declaración de todos los ítems que se van a leer o grabar, lo que no siempre es posible.

##### Estricto
Exige que no libere ningún *write lock* hasta después de terminar la transacción.
*Observación: Se hace unlock de los write lock después del commit.*
- Garantiza historias estrictas
- Susceptible a Deadlock

##### Riguroso
Exige que no se libere ningún *write/read lock* hasta después de terminar la transacción.
*Observación: Se hace unlock de los write/read lock después del commit.*
- Susceptible a Deadlock
