Un *autómata con salida* es una variación de los [[Autómata Finito]], pues los autómatas con salida no poseen un conjunto de estados de aceptación. Además, a medida que consumen la secuencia de entrada, producen una secuencia de salida.

Definimos una *autómata con salida* como $M=(Q, \Sigma, \Delta, \delta, \lambda, q_0)$ donde:
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\Delta$ un [[Alfabeto]] de salida.
- $\delta$ la función de transición.
- $\lambda$ la función de salida.
- $q_0 \in Q$ el estado inicial.

*La función de salida puede estar determinada por el estado actual y/o el símbolo de entrada actual.*
