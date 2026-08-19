# Trabajo Práctico N° 2: Redes de Computadoras

**Integrantes:**
* Arias, Daniel Andrés
* Garzón, Pablo
* Gutierrez, Patricio
* Fernández y Fernández, Sergio Ezequiel
* Loza Denardi, Gabriel Jeremías
* Rocatagliatta, Leandro Agustin
* Zambellini, Matías Manuel

---

# Inciso 1

**a)** En la figura se representa el fenómeno conocido como **Efecto Doppler** en ondas electromagnéticas. Que es el cambio aparente en la frecuencia de la onda debido al movimiento relativo entre la fuente emisora y el receptor. En cuanto a sus principales características se encuentran:

* **1) Movimiento relativo:** Es necesario que exista una velocidad de movimiento relativa entre el emisor y el receptor. Si ambos se mueven a la vez y a la misma velocidad, el fenómeno no se manifiesta.
* **2) Compresión/Dilatación de la onda:** Cuando el emisor y el receptor se aproximan entre sí, los frentes de onda se comprimen produciendo un aumento en la frecuencia percibida y menor longitud de onda (sonido más agudo). Cuando se alejan, los frentes se distancian produciendo una disminución en la frecuencia percibida y mayor longitud de onda (sonido más grave).
* **3) Universalidad ondulatoria:** Es capaz de afectar a cualquier tipo de movimiento ondulatorio.

**b)** Las bandas de transmisión más afectadas por este fenómeno son las de alta frecuencia (`UHF` - `SHF` - `EHF`) desde $1\text{ GHz}$ a $30\text{ GHz}$. Esto se debe a que el corrimiento absoluto está dado por la expresión $\Delta f = f0\cdot\frac{Vr}{c}$, directamente proporcional a la frecuencia de la portadora $f0$; donde puede verse que a mayor frecuencia, mayor es el corrimiento en $\text{Hz}$.
Las bandas más resilientes son las de baja y media frecuencia (`LF` - `MF` - `HF` - `VHF`) por debajo de los $300\text{ MHz}$. Esto es porque al ser la frecuencia de la portadora más baja, el corrimiento es menor.

**c)** La principal razón por la que no debe encenderse el teléfono móvil arriba de un avión es porque estos operan a potencias de transmisión variables. Al perder la cobertura en el aire, el celular aumenta al máximo su potencia buscando una estación base; esto podría acoplar interferencias parásitas en los sistemas de radionavegación, comunicaciones y altímetros de la aeronave.
El Efecto Doppler sí tiene que ver con este proceso, ya que el avión al viajar a velocidad muy altas genera un fuerte Efecto Doppler en el celular con las antenas en la tierra; esto provoca que las señales no puedan sincronizarse correctamente.

---

# Inciso 2

**a)** En la figura se representa el fenómeno conocido como **Ruido Impulsivo**. Es generado por la conmutación de corrientes elevadas, chispas o arcos eléctricos en motores con escobillas, relés, líneas de alta tensión o descargas atmosféricas (rayos). En cuanto a sus principales características se encuentran:

* **1) Duración breve:** Duran desde unos pocos microsegundos hasta milisegundos.
* **2) Amplitud elevada:** Presentan picos de voltaje o corriente mucho más altos que la señal útil o el ruido de fondo.
* **3) Amplio ancho de banda:** Su energía se distribuye en un espectro de frecuencias muy amplio.
* **4) Carácter aleatorio:** Su aparición es difícil de predecir. Se presentan en ráfagas aisladas o trenes de pulsos.

**b)** Las bandas de transmisión más afectadas por este fenómeno son las de baja y media frecuencia (`LF` - `MF` - `HF` - `VHF`), los medios guiados de cobre  sin blindaje y las modulaciones basadas en variaciones de amplitud (`AM` - `ASK`). Esto se debe a que la densidad de potencia del ruido electromagnético artifical se concentra principalmente en frecuencias menores a $1\text{ GHz}$. En cuanto a las bandas más resilientes, se incluyen las de frecuencia alta (`UHf` - `SHF`), las transmisiones ópticas (fibra óptica por ejemplo) y las modulaciones basadas en variaciones de frecuencia/fase (`PSK` - `QAM`); ya que allí, la densidad del ruido impulsivo es mucho menor.

**c)** La `SNR` (**Signal-to-Noise Ratio**) es una medida adimensional que cuantifica la calidad del canal de transmisión comparando la potencia de la señal transmitida con la potencia del ruido presente. Está dada por la fórmula:

$$SNR = \frac{Pseñal}{Pruido}$$

A menudo se expresa en decibelios mediante la expresión:

$$SNRdb = 10\cdot\text{log10}(\frac{Pseñal}{Pruido})$$

Además, la `SNR` y el `BER` guardan una relación inversa. Un valor elevado de `SNR` garantiza que la señal útil predomine sobre el ruido. Esto permite al demodulador tomar decisiones correctas en el muestreo de cada bit y reduce el `BER` a valores mínimos. Si la `SNR` decae (debido a atenuación o picos de ruido como el impulsivo), la probabilidad de interpretar erróneamente un estado lógico aumenta, elevando el `BER`.

---

# Inciso 3



---

# Inciso 4



---

# Inciso 5

