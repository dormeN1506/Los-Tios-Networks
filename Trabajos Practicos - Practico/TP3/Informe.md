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

**a)** La capa de enlace es la encargada de permitir la comunicación entre dispositivos que se encuentran dentro de una misma red local. Para hacerlo, toma la información que recibe de la capa de red y la organiza en tramas, agregando información necesaria para que pueda ser enviada por el enlace. Además, utiliza las direcciones MAC para identificar al dispositivo de origen y al dispositivo de destino dentro de esa red local. De esta forma, resuelve la comunicación entre nodos conectados al mismo enlace.

**b)** Una dirección MAC es una identificación que utiliza la capa de enlace para reconocer una interfaz de red dentro de una red local. Sirve para que las tramas puedan llegar al dispositivo correcto dentro de ese enlace. En cambio, la dirección IP pertenece a la capa de red y permite identificar lógicamente el origen y el destino de una comunicación, incluso cuando los equipos se encuentran en redes distintas. Por eso, la MAC se utiliza principalmente para la comunicación local, mientras que la IP permite la comunicación entre distintas redes. Por ejemplo, si mi computadora quiere comunicarse con un servidor en Internet, la MAC destino de la trama normalmente será la del router o gateway, mientras que la IP destino será la del servidor final.

**c)** Una trama Ethernet es la unidad de información que utiliza la capa de enlace para transportar datos dentro de una red local. La capa de enlace toma el paquete proveniente de una capa superior, por ejemplo un paquete IP, y lo encapsula, agregándole información necesaria para su direccionamiento, identificación y control durante la transmisión.
Sus campos principales son:

* Preámbulo: permite que el receptor se sincronice antes de comenzar a leer la trama.
* Dirección MAC destino: identifica la interfaz de red a la que debe llegar la trama dentro del enlace local.
* Dirección MAC origen: identifica la interfaz que envió la trama.
* EtherType o Tipo: indica qué protocolo de capa superior está encapsulado dentro de la trama, por ejemplo IPv4, IPv6 o ARP.
* Datos o Payload: contiene la información transportada, normalmente un paquete de capa de red como IP.
* FCS/CRC: permite detectar errores que hayan ocurrido durante la transmisión de la trama.

**d)** El campo EtherType permite identificar qué protocolo de capa superior está siendo transportado dentro de la trama Ethernet. Por ejemplo, puede indicar que el contenido corresponde a IPv4, IPv6 o ARP. De esta manera, el receptor sabe cómo interpretar los datos encapsulados y a qué protocolo entregarlos.

# Inciso 2
## Análisis con Wireshark

Se seleccionó una trama Ethernet con un paquete IPv6 encapsulado.

![Captura utilizada para el análisis](Multimedia/Ejercicio2.png)

**a)** *Direcciones MAC de origen y destino*

En la trama Ethernet seleccionada, la dirección MAC de origen es 04:7c:16:42:ae:b4, identificada por Wireshark como MicroStarINT_42:ae:b4, correspondiente a la interfaz de red de nuestra computadora.
La dirección MAC de destino es f8:79:28:96:a5:7e, identificada por Wireshark como zte_96:a5:7e. Esta corresponde al router ZTE de nuestra red local, que en esta comunicación funciona como gateway para poder salir hacia Internet.

**b)** *Direcciones IP de origen y destino*

Dentro de la trama Ethernet se encuentra encapsulado un paquete IPv6. La dirección IPv6 de origen corresponde a nuestra computadora (2803:9800:..., censurada en la captura), mientras que la dirección IPv6 de destino es 2800:3f0:4002:815::200a, correspondiente al host remoto con el cual se está realizando la comunicación.

**c)** *Comparación entre MAC e IP*

Las direcciones MAC y las direcciones IP no representan lo mismo. Las direcciones MAC trabajan en la capa de enlace y se utilizan para entregar la trama dentro del enlace o red local. En cambio, las direcciones IP trabajan en la capa de red e identifican el origen y el destino de la comunicación a través de distintas redes.
En nuestra captura se puede observar esta diferencia: la MAC destino corresponde al router ZTE, ya que es el siguiente dispositivo al que nuestra computadora debe entregar la trama dentro de la red local, mientras que la IPv6 destino corresponde al servidor remoto al que realmente queremos llegar a través de Internet.

**d)** *EtherType*

El campo EtherType de la trama tiene el valor 0x86dd, lo que indica que el protocolo encapsulado dentro de la trama Ethernet es IPv6. De esta manera, al recibir la trama, la capa de enlace puede determinar que los datos contenidos deben ser procesados por el protocolo IPv6 de la capa de red.
