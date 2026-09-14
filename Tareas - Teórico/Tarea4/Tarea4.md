# Redes de Computadoras

## Introducción
En el presente trabajo se realizará un breve repaso del capítulo 4 del libro *Stallings - Comunicaciones y Redes de Computadores, 7.ª edición*. Se abordarán los medios de transmisión, la propagación de ondas electromagnéticas y la relación entre frecuencia, longitud de onda, distancia y tamaño de las antenas.


### Ejercicio 4.5

La pérdida de propagación en el espacio libre se calcula mediante:

L = 10 × log10((4 × π × d / λ)^2)

La longitud de onda se relaciona con la frecuencia mediante:

λ = c / f

Reemplazando esta relación en la fórmula de pérdida:

L = 10 × log10((4 × π × d × f / c)^2)

Si se duplica la frecuencia:

f2 = 2 × f1

La diferencia entre las pérdidas es:

L2 - L1 = 20 × log10(f2 / f1)
L2 - L1 = 20 × log10(2)
L2 - L1 = 6,02 dB

Al duplicar la distancia ocurre lo mismo:

d2 = 2 × d1

L2 - L1 = 20 × log10(d2 / d1)
L2 - L1 = 20 × log10(2)
L2 - L1 = 6,02 dB

Por lo tanto, duplicar la frecuencia o la distancia aumenta la pérdida en aproximadamente 6 dB. Esto equivale a reducir la potencia recibida a la cuarta parte.

### Ejercicio 4.6

La frecuencia de transmisión es:

f = 30 Hz

La longitud de onda se calcula como:

λ = c / f
λ = (3 × 10^8) / 30
λ = 1 × 10^7 m

La antena debe medir aproximadamente la mitad de la longitud de onda:

l = λ / 2
l = (1 × 10^7) / 2
l = 5 × 10^6 m
l = 5000 km

La antena debería tener una longitud aproximada de 5000 km.

### Ejercicio 4.7
a) Antena para una señal de 300 Hz

La longitud de la antena debe ser igual a la mitad de la longitud de onda:

l = λ / 2
l = c / (2 × f)

Reemplazando la frecuencia:

l = (3 × 10^8) / (2 × 300)
l = (3 × 10^8) / 600
l = 5 × 10^5 m
l = 500 km

Para transmitir directamente una señal de 300 Hz, la antena debería medir aproximadamente 500 km.

b) Frecuencia portadora para una antena de 1 metro

Si la antena mide 1 m y representa la mitad de la longitud de onda:

l = λ / 2
λ = 2 × l
λ = 2 × 1
λ = 2 m

La frecuencia de la portadora se calcula como:

f = c / λ
f = (3 × 10^8) / 2
f = 1,5 × 10^8 Hz
f = 150 MHz

La frecuencia portadora necesaria es de 150 MHz.

### Ejercicio 4.8

El empaste tiene una longitud de:

l = 2,5 mm
l = 0,0025 m

Como su longitud representa la mitad de la longitud de onda:

l = λ / 2
λ = 2 × l
λ = 2 × 0,0025
λ = 0,005 m

La frecuencia correspondiente es:

f = c / λ
f = (3 × 10^8) / 0,005
f = 6 × 10^10 Hz
f = 60 GHz

Según el modelo ideal del ejercicio, el empaste recibiría una señal de aproximadamente 60 GHz.
