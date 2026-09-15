# Redes de Computadoras

## Introducción
En el presente trabajo se realizará un breve repaso del capítulo 4 del libro *Stallings - Comunicaciones y Redes de Computadores, 7.ª edición*. Se abordarán los medios de transmisión, la propagación de ondas electromagnéticas y la relación entre frecuencia, longitud de onda, distancia y tamaño de las antenas.

### Ejercicio 4.1

Supóngase que unos datos se almacenan en disquetes de 1,4 Mbytes que pesan 30 g cada uno y que una compañía aérea transporta 10^4 kg de disquetes a una velocidad de 1.000 km/h

sobre una distancia de 5.000 km. ¿Cuál es la velocidad de transmisión en bits por segundo
de este sistema?

Tenemos estos datos:
- Cantidad de Mbytes por disquetes: 1,4 Mbytes
- Peso total: 10.000 kg de disquetes
- Peso de cada disquete: 30 g = 0,03 kg
- velocidad ***(v)***: 1.000 km/h

Cantidad de disquetes =  ${ \frac{10000}{0,03} ≈ 333,33\  disquetes }$

Cantidad de bits por disquetes = ${ 1,4\  bits × 10⁶\ bytes × 8 = 11200000\ bits = 11,2 × 10⁶\  bits }$

Cantidad de bits en total = ${ 333,33 × 11,2 × 10⁶ =  3,73 × 10¹² bits }$

${ t = \frac{d}{v} = \frac{5000 km}{1000 km/h} = 5h }$

${ t = 5 × 3600 seg = 18000 seg }$

${ velocidad  = \frac{3,73 × 10¹²}{18000} ≈ 2,07 × 10^8 bits/s ≈ 207Mpbs }$

### Ejercicio 4.2

Sea una línea telefónica caracterizada por una pérdida de 20 dB. La potencia de la señal a
la entrada es de 0,5 W y el nivel del ruido a la salida es de 4,5 W. Calcule la relación
señal ruido para la línea en dB.

Tenemos estos datos:
- pérdida: 20dB.
- ${ P_{entrada} = 0,5 \ W }$
- ${ P_{salida} = 4,5 \ W }$

Potencia de salida:

${ L_{dB}=10\log(\frac{P_{entrada}}{P_{salida}}) }$

${ P_{salida}=P_{entrada} × 10^{-L/10} =0,5 × 10^{-20/10} =0,5 × 10^{-2}=0,005\ W }$

Relación S/N:

${ SNR=\frac{P_S}{P_N} =\frac{0,005}{4,5}=0,001111 }$

Pasamos a dB:

${ SNR_{dB}=10\log(0,001111) }$

${ SNR_{dB}\approx -29,54\ dB }$

El resultado negativo nos indica que la potencia del ruido es mucho mayor que la potencia de la señal de salida por lo que la señal queda prácticamente tapada por el ruido.


### Ejercicio 4.3

Datos:

- ${ P_{Transmisión}=100 \ W }$
- ${ P_{Recepción}=1 \ W }$

| Medio | Frecuencia | Atenuación |
|---|---:|---:|
| Par trenzado (con carga)| 0 a 3,5 kHz | 0,2 dB/km |
| Par trenzado (cables multi-pares) | 0 a 1 MHz | 3 dB/km |
| Coaxial | 0 a 500 MHz | 7 dB/km |
| Fibra óptica | 180 a 370 THz | 0,2 a 0,5 dB/km |


Pérdida máxima: ${ 10\log(\frac{P_{Transmisión}}{P_{Recepción}}) = 10\log(\frac{100}{1}) = 20 \ dB }$

Longitud máxima L: ${ \frac{20}{\alpha} }$

a). L =  ${ \frac{20}{3} = 6,67 \ Km }$

b). L =  ${ \frac{20}{3} = 6,67 \ Km }$

c). L =  ${ \frac{20}{7} = 2,86 \ Km }$

d). L =  ${ \frac{20}{7} = 2,86 \ Km }$

d). L =  ${ \frac{20}{7} = 2,86 \ Km }$

e). L =  ${ \frac{20}{7} = 0,2 \ Km }$


### Ejercicio 4.4

La malla del coaxial, al estar conectada a tierra, actúa como blindaje y reduce las interferencias electromagnéticas externas y la diafonía, mejorando la calidad de la señal transmitida.

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
