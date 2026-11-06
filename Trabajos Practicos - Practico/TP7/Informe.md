# Trabajo Práctico N° 7: Redes de Computadoras

**Integrantes:**
* Arias, Daniel Andrés
* Garzón, Pablo
* Gutierrez, Patricio
* Fernández y Fernández, Sergio Ezequiel
* Loza Denardi, Gabriel Jeremías
* Rocatagliatta, Leandro Agustin
* Zambellini, Matías Manuel

**Grupo:** Los-Tios-Networks  
**Fecha de la experiencia:** 29/10/2026

---

## PARTE 1: Desafío final — Captura, decodificación y recuperación de datos

### Inciso 1. Direccionamiento IP y difusión (*broadcast*)

Durante el laboratorio se utilizó una red Wi-Fi proporcionada por la cátedra. El objetivo consistió en detectar mensajes de difusión emitidos hacia todos los equipos del dominio de broadcast de la red local.

En la **captura obtenida** se identificaron los siguientes campos de los paquetes relevantes:

| Parámetro | Valor observado |
|---|---|
| IP de origen del emisor | `192.168.8.150` |
| IP de destino del paquete | `192.168.8.255` |
| MAC de origen | `DC:90:09:ED:91:35` |
| MAC de destino | `FF:FF:FF:FF:FF:FF` |
| Protocolo de transporte | UDP |
| Puertos UDP (origen → destino) | `63573 → 12007` |

La dirección MAC `FF:FF:FF:FF:FF:FF` es el valor reservado para **broadcast Ethernet**. La dirección IPv4 `192.168.8.255` es compatible con el broadcast dirigido de la red `192.168.8.0/24`, **si la máscara utilizada era `/24`**. No es posible afirmar solamente por observar esa dirección cuál era la máscara configurada en nuestra computadora.

**Dato pendiente:** no se conserva todavía una salida de `ipconfig` que permita documentar con certeza la dirección IPv4 y la máscara de la notebook utilizada. En el archivo de captura se ven solicitudes DHCP con dirección solicitada `192.168.8.180`, pero ese dato no confirma que haya sido la configuración finalmente asignada. Es necesario completar este inciso con una evidencia de la configuración local, si está disponible.

**Esquema de la comunicación observada:**

![Esquema de difusión UDP](Multimedia/01_esquema_broadcast.svg)

### Inciso 2. Captura de tráfico con Wireshark

Se inició una captura sobre la interfaz Wi-Fi de la computadora del grupo durante la actividad presencial. La captura se guardó en formato `.pcapng` para permitir el análisis posterior, conservando las tramas y sus encabezados originales.

| Dato | Resultado |
|---|---|
| Archivo original | `captura 1.pcapng` |
| Intervalo aproximado | 29/10/2026, 18:59:04–19:09:16 (UTC−3) |
| Duración total | **611,7 s**, aproximadamente **10 min 12 s** |
| Tramas registradas | **7.033** |
| Tramas con JSON relacionadas con la actividad | **22** |
| Trama de ejemplo con la variante binaria | **228** |

La captura supera los **2 minutos mínimos** establecidos en la consigna. Para aislar los mensajes del desafío se pueden utilizar, entre otros, estos filtros de visualización:

```wireshark
udp.srcport == 63573 && udp.dstport == 12007
```

```wireshark
frame contains "SIZE"
```

Estos filtros **no deben confundirse con filtros de captura**: sirven para visualizar paquetes ya registrados sin eliminar el tráfico guardado.

**Evidencia disponible:** el archivo `.pcapng` original, que se debe adjuntar por el canal de entrega autorizado si la cátedra lo requiere. **No se incorpora a este repositorio público**, porque la captura también contiene tráfico de otros equipos ajenos a la actividad.

### Inciso 3. Análisis del formato y la estructura del mensaje

Al inspeccionar la carga útil UDP se observó texto estructurado en formato **JSON**. El mensaje relevante utiliza tres campos:

- **`SIZE`:** indica las dimensiones declaradas de la matriz. En la variante analizada, `"8,7"`.
- **`PL`:** secuencia de caracteres ASCII `0` y `1` que representa los bits de información. Los caracteres no se transmiten como bits individuales empaquetados en el JSON, sino como texto.
- **`CHECK`:** secuencia de bits de control: primero las paridades de fila y luego las de columna.

El valor `SIZE = "8,7"` se interpretó, de acuerdo con el formato recibido y el comportamiento del decodificador, como **8 filas**, cada una con **7 caracteres de 7 bits**, es decir, **49 bits de datos por fila**. Así:

- Datos (`PL`): `8 × 7 × 7 = 392` bits representados por caracteres `0`/`1`.
- Paridades de fila: `8` bits.
- Paridades de columna: `49` bits.
- Total de control (`CHECK`): `8 + 49 = 57` bits.

Se encontraron diferentes cargas útiles JSON en la captura:

| Variante | Tramas | Análisis |
|---|---:|---|
| `SIZE = "8,7"`, `PL` binario de 392 caracteres, `CHECK` de 57 | 6 | Coherente con el esquema de paridad propuesto. |
| `SIZE = "99,9"`, campos con texto de URL | 4 | No contiene las longitudes binarias esperadas. |
| `SIZE = "N,M"`, `PL` con una URL | 6 | Las dimensiones no son numéricas. |
| `SIZE = "2,23"`, `PL` con una URL | 6 | Dimensiones y longitud del contenido incompatibles. |

Se seleccionó la primera variante para su verificación binaria, dejando identificados los demás mensajes como variantes **no compatibles con el formato de paridad analizado**. La consigna advierte que los mensajes recibidos no tienen que ser idénticos.

El objeto JSON original, sin comentarios, está disponible en [el archivo de evidencia](Multimedia/TP7_payload_original_limpio.json).

### Inciso 4. Verificación mediante paridad bidimensional

Para realizar la comprobación se extrajeron los bits de `PL` y se dividieron en 8 filas de 49 bits cada una. El script `paridad.py` proporcionado por la cátedra permite calcular la **paridad par** de cada fila y columna. Luego se compararon las paridades calculadas con `CHECK`.

Las secuencias de control fueron:

| Control | Recibido en `CHECK` | Calculado desde `PL` |
|---|---|---|
| Filas (8 bits) | `01111101` | `01110011` |
| Columnas (49 bits) | `0110111111110110011100101111001100001100110010001` | `0110111101110110111100001111001100001100110010001` |

Se identificaron las siguientes discrepancias (*síndrome de paridad bidimensional*):

- **Filas:** 5, 6 y 7.
- **Columnas:** 9, 17 y 23.

El resultado indica que los datos recibidos no son consistentes con las paridades transmitidas. A diferencia del caso de un único error, la presencia de varias filas y columnas discordantes no identifica un conjunto único de bits erróneos: existen distintas combinaciones de intersecciones que podrían producir el mismo síndrome.

**Matriz original y verificación completa:**

- [Matriz original](Multimedia/TP7_matriz_original.txt).
- [Paridades recibidas](Multimedia/TP7_paridades_recibidas.txt).
- [Cálculo y comparación de paridades](Multimedia/TP7_verificacion_paridades.txt).

### Inciso 5. Ubicación y corrección de los errores

Se eligió una corrección compatible con el síndrome y que, además, permite reconstruir un texto ASCII coherente. Las posiciones se numeran **desde 1**, comenzando por la primera fila y la primera columna de la matriz de bits.

| Fila | Columna | Bit recibido | Bit corregido |
|---:|---:|:---:|:---:|
| 5 | 9 | `1` | `0` |
| 6 | 17 | `0` | `1` |
| 7 | 23 | `0` | `1` |

![Matriz con los tres bits corregidos resaltados](Multimedia/02_matriz_paridad.svg)

Tras invertir esos tres bits, se recalcularon todas las paridades. **Las 8 paridades de fila y las 49 de columna coinciden con `CHECK`.**

Esta coincidencia confirma que la matriz corregida es **consistente con los controles recibidos**. Sin embargo, no demuestra que sea la **única corrección posible**, porque la paridad bidimensional puede ser ambigua frente a múltiples errores.

**Archivo de evidencia:** [matriz corregida](Multimedia/TP7_matriz_corregida.txt).

### Inciso 6. Decodificación del mensaje corregido

Una vez corregidos los datos, se guardaron las ocho filas de 49 bits en un archivo de texto, una por línea y sin los bits de control. Se utilizaron los scripts de la cátedra:

```powershell
py paridad.py TP7_matriz_corregida.txt
py decodificar_mensaje.py TP7_matriz_corregida.txt
```

El decodificador interpreta cada grupo de siete bits como un carácter ASCII y cada línea de forma independiente. El texto, concatenando las líneas y quitando espacios de relleno al final, es:

```text
https://youtube.com/shorts/q8WgKzJwPa4?feature=share
```

Por lo tanto, la carga útil reconstruida contiene **un enlace web**. En el análisis no se asume ni se describe el contenido del sitio enlazado: el resultado comprobado es la secuencia de texto obtenida a partir de los bits y la consistencia de las paridades.

### Inciso 7 (opcional). Automatización del análisis de paridad

El script `paridad.py` calcula los bits de control, pero no los compara automáticamente con el campo `CHECK` de un JSON. En este análisis se realizó la comparación de las dos secuencias de control y se registraron por separado las discrepancias de filas y columnas en [el archivo de verificación](Multimedia/TP7_verificacion_paridades.txt).

---

## PARTE 2: Reflexiones e investigación

### Inciso 1. Errores simultáneos y errores en bits de control

**a) Dos bits de datos alterados en distintas filas y columnas.** Fallan dos controles de fila y dos controles de columna. Se forman **cuatro intersecciones candidatas**, por lo que no es posible decidir inequívocamente qué dos bits cambiaron utilizando únicamente esas paridades. Si ambos errores estuvieran en la misma fila, la paridad de esa fila podría coincidir y fallarían dos controles de columna.

También existen errores múltiples no detectados: por ejemplo, la inversión de las cuatro esquinas de un rectángulo conserva la paridad de todas las filas y columnas.

**b) Un bit de control alterado.** Si se invierte exclusivamente un bit de paridad de fila, falla ese control sin que falle ninguna paridad de columna. De manera análoga, un bit de control de columna alterado puede producir una discrepancia solamente en una columna. Esto permite sospechar un error en el control, aunque el diagnóstico no es necesariamente único si también se permiten varios errores en los datos.

### Inciso 2. Limitaciones de la recuperación por contexto

Al recuperar texto, la coherencia lingüística puede ayudar a elegir una corrección plausible, pero **no garantiza la integridad de la información**. Una URL, una contraseña o un número de cuenta pueden cambiar por un solo carácter y conservar una apariencia válida.

La utilidad de los bits de control es ofrecer una verificación **independiente de la interpretación del mensaje**. En nuestra experiencia, la lectura coherente permitió proponer una corrección y las paridades confirmaron su consistencia. Esta comprobación no debe confundirse con una garantía absoluta de recuperación cuando hay varios errores.

### Inciso 3. Confirmación de la corrección realizada

La comprobación consistió en recalcular, sobre el archivo corregido, los **8 bits de paridad de fila** y los **49 de columna**. Los 57 bits coincidieron con el campo `CHECK` original del paquete recibido. Además, la conversión ASCII produjo una cadena legible con estructura de URL.

Ambos resultados apoyan la corrección seleccionada, pero reconocemos que el código de paridad 2D **no garantiza unicidad de recuperación** para el patrón de errores múltiple observado.

### Inciso 4. Investigación y aplicación de Hamming (7,4)

El código **Hamming (7,4)** transforma cuatro bits de información en siete bits, agregando tres bits de paridad. En la distribución convencional con paridad par, las posiciones son:

| Posición | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| Tipo | `p1` | `p2` | `d1` | `p4` | `d2` | `d3` | `d4` |

Cada bit de paridad cubre las siguientes posiciones:

- `p1`: 1, 3, 5 y 7.
- `p2`: 2, 3, 6 y 7.
- `p4`: 4, 5, 6 y 7.

La paridad es **par**: el XOR de los bits cubiertos por cada control debe dar cero. En el receptor se calculan tres comprobaciones (`s1`, `s2`, `s4`) y se forma el síndrome binario `s4s2s1`. Si el síndrome es distinto de cero y se supone **un único bit erróneo**, su valor en decimal indica la posición que debe invertirse. Si el síndrome es `000`, no se detecta un error.

**Ejemplo:** al codificar los datos `1101`, resulta la palabra `1010101`. Si se invierte el bit 5, el síndrome es `101₂ = 5`; al invertir ese bit nuevamente, se recupera la palabra original.

Hamming (7,4) tiene **distancia mínima 3**, por lo que permite corregir un error por palabra de siete bits y detectar hasta dos errores, aunque no corrige de forma fiable dos errores en una misma palabra. Ante dos errores, un decodificador que siempre intente corregir según el síndrome puede producir una corrección errónea.

**Aplicación al mensaje de la práctica.** Se eligió codificar la secuencia de bits **`PL` corregida**, y no la representación textual del JSON completo. Como contiene 392 bits:

```text
392 bits de datos / 4 bits por bloque = 98 bloques
98 bloques × 7 bits Hamming = 686 bits protegidos
Bits agregados de control = 686 − 392 = 294
Relleno necesario = 0 bits
```

Se codificaron los 98 bloques de 4 bits consecutivos aplicando Hamming (7,4). El paquete propuesto incorpora la secuencia protegida y metadatos para que el receptor pueda interpretarla:

- [Paquete codificado en JSON](Multimedia/TP7_paquete_hamming74.json).
- [Bloques codificados de Hamming](Multimedia/TP7_hamming_74_bloques.txt).

La superioridad de Hamming respecto del esquema didáctico aplicado en este TP se refiere a que **localiza y corrige un error por palabra** sin requerir una matriz global. No es superior en todos los aspectos: para estos 392 bits, Hamming (7,4) agrega **294 bits de control**, mientras que la paridad bidimensional original requiere **57 bits**, y ambos esquemas tienen límites frente a patrones de errores múltiples.

---

## Conclusiones

La actividad permitió capturar y analizar tráfico de difusión UDP en una red local, identificar un mensaje estructurado como JSON y reconstruir la matriz binaria transportada en su carga útil. Las verificaciones de paridad detectaron discrepancias en tres filas y tres columnas, lo que motivó una corrección consistente de tres bits.

La matriz corregida reprodujo los 57 bits de control recibidos y pudo decodificarse como una URL. También se construyó una propuesta de codificación con Hamming (7,4) para contrastar dos métodos de detección y recuperación de errores.

La experiencia mostró la utilidad de los códigos de control y, a la vez, **la importancia de distinguir una corrección consistente de una recuperación matemáticamente única**.

---

## Archivos de evidencia y aspectos pendientes

Los archivos de trabajo que acompañan este informe se encuentran en `Multimedia/`:

| Archivo | Contenido |
|---|---|
| `TP7_payload_original_limpio.json` | Mensaje JSON de la variante binaria válida. |
| `TP7_matriz_original.txt` | Bits recibidos, distribuidos en 8 filas de 49. |
| `TP7_matriz_corregida.txt` | Matriz con las tres correcciones propuestas. |
| `TP7_paridades_recibidas.txt` | Bits de paridad originales. |
| `TP7_verificacion_paridades.txt` | Comparación de paridades y posiciones discrepantes. |
| `TP7_paquete_hamming74.json` | Propuesta de paquete protegido con Hamming (7,4). |
| `TP7_hamming_74_bloques.txt` | Las 98 palabras Hamming de 7 bits. |

**Pendiente de completar antes de la entrega:** confirmar mediante `ipconfig` la IP y la máscara de la notebook durante la experiencia; registrar la comisión y, si corresponden, los legajos; adjuntar una captura de Wireshark de la trama 228 o entregar el `.pcapng` completo por un medio privado autorizado; y corroborar con el equipo los datos administrativos y el procedimiento utilizado.

**Privacidad:** el archivo de captura original incluye tráfico de terceros, por lo que se conserva para una entrega privada al docente y no se publica como evidencia abierta en el repositorio.
