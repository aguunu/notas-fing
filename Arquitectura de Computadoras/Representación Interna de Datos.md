## Entero
### Con Signo
TODO

### Sin Signo
TODO

## Desplazamiento
TODO

## Complemento a 1
TODO

## Complemento a 2
TODO

## BCD
TODO

## Decimal
TODO

## Punto Flotante
$N = (-1)^s \cdot b^e \cdot M$ 
- $s$ : signo
- $e$ : exponente
- $b$ : base
- $M$ : mantisa

### IEEE 754 Normalizada
Se utiliza $b=2$ y la mantisa normalizada es de la forma 1,F. Mientras que la mantisa des-normalizada es de la forma 0,F.

| |S|E|F|Total (bits)|
|---|---|---|---|---|
|Simple|1|8|23|32|
|Doble|1|11|52|64|
|Media|1|5|10|2|

El desplazamiento se calcula de la siguiente manera: $D = 2^{E - 1} - 1$

| |E|F|
|---|---|---|
|Normalizado|$0...0 \leq E < 1...1$|Cualquiera|
|Desnormalizado|$0...0$|$\neq 0$|
|Cero|$0...0$|$0$|
|Infinito|$1...1$|$0$|
|NaN|$1...1$|$\neq 0$|

