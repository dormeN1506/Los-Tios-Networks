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
