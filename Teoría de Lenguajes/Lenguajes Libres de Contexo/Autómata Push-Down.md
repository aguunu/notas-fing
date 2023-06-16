Una *autómata push-down (APD)* es un autómata cuyo comportamiento es similar al de un [[Autómata Finito]] que dispone de una *stack*, pasando a tener una cantidad *ilimitada* de memoria.

Definimos un *APD* como $M=(Q,\Sigma,\Gamma,\delta, q_0, Z_0, F)$ donde,
- $Q$ un conjunto finito de estados.
- $\Sigma$ un [[Alfabeto]] de entrada.
- $\Gamma$ el [[Alfabeto]] de la *stack*.
- $\delta : Q \times (\Sigma \cup \{ \varepsilon \}) \times \Gamma \rightarrow 2^{Q + \Gamma^\star}$ la función de transición tal que
	$\delta(q, a, X) = \{(p_1, \alpha_1),...,(p_n, \alpha_n)\}$ con $\alpha_i = \begin{cases} RX, & \text{  apilar R sobre X. } \\ X, & \text{ mantener X en el tope. } \\ \varepsilon, & \text{ desapilar X. } \end{cases}$
	donde $p_i \in Q, a \in (\Sigma \cup \{ \varepsilon \}), R, X \in \Gamma$. 
- $q_0 \in Q$ el estado inicial.
- $Z_0 \in \Gamma$ el símbolo inicial del *stack*.
- $F \subseteq Q$ el conjunto de estados finales.

***

## Descripción Instantánea
Sea $M=(Q,\Sigma,\Gamma,\delta, q_0, Z_0, F)$ un APD. Definimos una *descripción instantánea* $(q,w,\alpha)$ de forma que:
- $q \in Q$ es el estado actual.
- $w \in \Sigma^\star$ es lo que resta por leer de la entrada.
- $\alpha \in \Gamma^\star$ es el contenido actual del *stack*. (Convencionalmente el símbolo de más a la izquierda es el *tope* del *stack*).

Si $(p, \alpha) \in \delta(q, a, X)$ entonces, $(q, aw, X\beta) \vdash (p, w, \alpha \beta)$ representa que $M$ desde el estado $q$ al estado $p$ con la entrada $a$ cuando el tope del *stack* es $X$ y remplaza $X$ en el tope del *stack* por $\alpha$. 

*La notación $\vdash^\star, \vdash^n$ representa que dicho cambio ocurre en una cantidad indefinida o $n$ pasos.*

***

## Lenguaje Aceptado
Sea $M=(Q,\Sigma,\Gamma,\delta, q_0, Z_0, F)$ un APD, el *lenguaje aceptado* por $M$ por **estado final** es

$$L(M)=\{ x \in \Sigma^\star \mid (q_0, x, Z_0) \vdash^\star (q_f, \varepsilon, \alpha) \text{ con } q_f \in F \land \alpha \in \Gamma^\star \}$$

Sea $M=(Q,\Sigma,\Gamma,\delta, q_0, Z_0, \textcolor{red}{\emptyset})$ un APD, el *lenguaje aceptado* por $M$ por **stack vacío** es

$$L(M)=\{ x \in \Sigma^\star \mid (q_0, x, Z_0) \vdash^\star (q, \varepsilon, \varepsilon) \text{ con } q \in Q \}$$

>[!important] Equivalencia
>El lenguaje aceptado por *estado final* es equivalente al lenguaje aceptado por *stack vacío*.

***

## Determinista
Una APD es *determinista* si cumple con las siguientes condiciones:

$$\tag{1} \forall q \in Q, \forall a \in (\Sigma \cup \{ \varepsilon\}), \forall X \in \Gamma : |\delta(q,a,X)| \leq 1$$

$$\tag{2} \forall q \in Q, \forall X \in \Gamma: \text{ Si } |\delta(q, \varepsilon, X)| = 1 \text{ entonces } \forall b \in \Sigma : \delta(q, b , X) = \emptyset$$

***

>[!important]
>$L$ es un [[Gramáticas Libres de Contexto#Lenguaje Libre de Contexto|Lenguaje Libre de Contexto]] si es aceptado por algún [[Autómata Push-Down|APD]]. 
