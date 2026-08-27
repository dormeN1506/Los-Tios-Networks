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

Los sistemas de transmisión digital combaten los errores generados por el ruido del canal (como el ruido impulsivo o térmico) mediante la adición de redundancia controlada a la información original a nivel de software o hardware. Esto se implementa a través de dos enfoques principales:

* Detección: Se agregan bits adicionales a los datos transmitidos para verificar su integridad en el receptor. Ejemplos como el bit de paridad, sumas de verificación (Checksum) y el control de redundancia cíclica (CRC). Todos estos métodos de detección son realizados por el receptor, al aplicar el algoritmo de verificación, si obtiene un valor distinto al esperado, detecta que la trama fue corrompida.

* Corrección: Una vez detectado el error, el sistema puede recuperar la información de dos maneras. Mediante técnicas ARQ (Automatic Repeat reQuest), el receptor simplemente descarta la trama y solicita al emisor su retransmisión. En enlaces donde la retransmisión es inviable por alta latencia, se utilizan técnicas FEC (Forward Error Correction). Se emplean códigos matemáticos avanzados (como códigos de Hamming, Reed-Solomon o convolucionales) que entrelazan redundancia de tal forma que el receptor puede deducir exactamente qué bits cambiaron de estado y corregirlos. Esto es fundamental en enlaces donde la latencia hace inviable pedir una retransmisión.  
  
---

# Inciso 4



---

# Inciso 5

**a)** Nuestro nombre de grupo es 'Los-Tios-Network' si nos quedamos solo con los primeros 5 caracteres en lower case queda de la siguiente manera 'los-t' debemos pasarlo a hexadecimal para obtener nuestros 40 bits de GROUP:  **l = 0x6C, o = 0x6F, s = 0x73, - = 0x2D, t = 0x74**

<img width="843" height="99" alt="image" src="https://github.com/user-attachments/assets/baae4e7b-2576-4df4-9ae0-d99e1b80b94b" />

Una vez encontrado nuestro patrón, podemos determinar la trama que nos corresponde.

* Firma del grupo (GROUP): Los bytes resaltados en azul son 6c 6f 73 2d 74, que efectivamente corresponden a "los-t" en código ASCII.
* Número de secuencia (SEQ): El byte inmediatamente posterior a la firma es 0e resaltado en rojo. Si convertimos este valor hexadecimal a decimal, obtenemos 14. Esto significa que la información de este paquete va en la posición 14 del mensaje final.
* Longitud de la carga útil (LENGTH): El byte que le sigue a la secuencia es 01 en color verde. Esto nos indica que el payload que transporta este paquete tiene una longitud de exactamente 1 byte.
* Carga útil (PAYLOAD): Como la longitud es 1, tomamos solamente el byte siguiente el de color rosa, que es 63. Si traducimos el valor hexadecimal 63 a texto mediante la tabla ASCII, obtenemos la letra minúscula 'c'.

**b)** Si repetimos este proceso para todos los grupos extrayendo todos los payloads y reordenando de acuerdo al número de sequencia podremos obtener finalmente una url que nos envia a un short de YouTube `https://www.youtube.com/shorts/dbbe_ln6Lnw`.

Para automatizar la repetición del proceso nos válimos del siguiente script al que le pasamos un array con los 5 primeros caracteres de cada grupo:

```python

def find_and_reorder_payloads(targets):
    all_payloads = []

    with open('frames.bin', 'rb') as f:
        data = f.read()

    for target_bytes in targets:
        offset = data.find(target_bytes)

        if offset == -1:
            continue  # No se encontró este target, saltar al siguiente

        if offset + 7 > len(data):
            continue  # No hay espacio para SEQ + LENGTH

        seq = data[offset + 5]  # 1 byte después del target (5 bytes)
        length = data[offset + 6]  # 1 byte después del SEQ

        if offset + 7 + length > len(data):
            continue  # No hay espacio para el payload

        payload = data[offset + 7 : offset + 7 + length]
        all_payloads.append({
            'SEQ': seq,
            'PAYLOAD_STR': payload.decode('latin-1', errors='replace')
        })

    # Ordenar por SEQ
    all_payloads.sort(key=lambda x: x['SEQ'])

    # Concatenar los payloads en orden
    message = ''.join([p['PAYLOAD_STR'] for p in all_payloads])
    return message
```
