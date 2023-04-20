## Algoritmo de Minimización
Dado un [[Autómata Finito Determinista|AFD]] $M=(Q, \Sigma, \delta, q_0, F)$ obtendremos un AFDM $M'=(Q', \Sigma, \delta', q'_0, F')$.

1. Agregar $q_p$ el estado pozo.
2. Si hay algún estado inalcanzable eliminarlo.
3. $(i=0)$ Marcar todos los estados *distinguibles* con la cadena vacía (es decir, todos los finales se pueden distinguir de los no finales).
4. $(i=i+1)$ Marcar como *distinguibles* $q$ y $q'$ si con algún $a \in \Sigma$ obtenemos que $\delta(q,a)$ es distinguible de $\delta(q',a)$.
5. Si en el paso anterior se han distinguido nuevos estados, volver.

Sea $M=\{Q, \Sigma, \delta, q_0, F\}$ y además  $p, q \in Q$:
- **Estados Equivalentes**: $p$ es equivalente a $q$ si $\forall x \in \Sigma^\star: \hat{\delta}(p, x) \in F \iff \hat{\delta}(q,x) \in F$.
- **Estados Distinguibles**: $p$ es *distinguible* de $q$ si $\exists x \in \Sigma^\star: \hat{\delta}(p, x) \in F \land \hat{\delta}(q,x) \notin F$.

*Observación: $p$ y $q$ son distinguibles $\iff$ $p$ y $q$ no son equivalentes.*

## Myhill-Nerode
Si se construye un AFD donde cada clase de equivalencia $R_L$ tiene asociado un estado, ese autómata es el mínimo.

### Teorema
$L$ es un [[Lenguaje#Lenguaje Regular|Lenguaje Regular]] $\iff$ $|R_L|$ *(cantidad de clases de equivalencia) es finito.

### Colorario
Para todo [[Lenguaje#Lenguaje Regular|Lenguaje Regular]], existe y es único el AFDM (autómata finito determinado mínimo).