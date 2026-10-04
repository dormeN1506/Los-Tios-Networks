# Trabajo Práctico N° 5: Redes de Computadoras

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

**a)** ICMP (Internet Control Message Protocol) o Protocolo de Control de Mensajes de Internet, es un protocolo de la capa de red, el cual funciona como un sistema de diagnóstico y notificación de errores de una red. Dado que el protocolo IP por sí mismo no tiene un mecanismo para confirmar si un paquete se entregó con éxito, ICMP proporciona un medio para verificar que los dispositivos de una red se comuniquen correctamente. 
A diferencia de TCP y UDP, ICMP no transporta datos de aplicaciones. El payload de un mensaje ICMP contiene metadatos de control y diagnostico.

**b)** El protocolo ICMP viaja dentro de IP, encapsulado como su carga útil. El receptor lo identifica debido a que la cabecera del paquete IP tiene el campo "Protocolo" en el valor 1.

**c)** El comando ping verifica la conectividad y mide la latencia entre dispositivos enviando un mensaje de prueba llamado Echo Request (Petición eco) y esperando una confirmación del receptor llamada Echo Reply (Respuesta eco). Para distinguirlos se utiliza el campo "Tipo" siendo el valor 8 para el Request y 0 para el Reply y ambos utilizan el "Código" en valor 0. 

**d)** Un mensaje ICMP de tipo Echo contiene una cabecera mínima y obligatoria de exactamente 8 bytes, dividida en los siguientes cinco campos:

* **Tipo (8 bits):** Especifica el tipo de mensaje ICMP.
* **Código (8 bits):** Se usa para especificar parámetros del mensaje.
* **Checksum (16 bits):** Suma de comprobación para verificar la integridad del mensaje ICMP entero.
* **Identificador (2 bytes):** Un valor único que permite al emisor reconocer qué aplicación generó la solicitud.
* **Número de Secuencia (2 bytes):** Un contador que se incrementa en cada envío para poder emparejar exactamente cada respuesta con su pregunta original y calcular la latencia de ese paquete individual.

A continuación se mostrara el paso a paso que se realizo para poder capturar paquetes icmp por Wireshark y de donde obtenemos los datos para poder completar la tabla
![ipconfig](Multimedia/01_ipconfigall.png) ![ping](Multimedia/02_ping.png) ![request](Multimedia/03_filtrorequest.png) ![reply](Multimedia/04_filtroreply.png) ![google](Multimedia/05_filtrogoogle.png) ![ethernet2](Multimedia/06_ethernet2.png) ![ipv4](Multimedia/07_ipv4.png) ![payload](Multimedia/08_icmppayload.png) ![tabla](Multimedia/09_tabla.png)

**a)** En la imagen podemos ver que la MAC de destino es la misma que la de nuestro gateway (imágenes anteriores) ya que el alcance de una dirección MAC es meramente local. Con la dirección MAC de un dispositivo solo podremos ir hasta el siguiente router, cambiando cada vez que realice un salto, en cambio con la IP que viaja encapsulada en la trama esta si se mantendrá desde el origen hasta el final.
![mac](Multimedia/10_mac.png)

**b)** En Ethernet tenemos que las direcciones MAC de origen y de destino se invierten, pero se mantiene el campo Type ya que ambos siguen transportando un paquete IPv4. Para IP sucede lo mismo con las direcciones, estas están invertidas pero mantienen el mismo campo de protocolo. El campo Type de ICMP varia, siendo 8 para Echo Request y 0 para Echo Reply, el checksum cambia ya que se recalcula y los Identifier (BE/LE) y Sequence Number (BE/LE) se mantienen iguales, debido a que estos se utilizan para que el dispositivo pueda emparejar la petición que envió con la respuesta.
![seq](Multimedia/11_seq.png)

**c)** Como podemos ver en la imagen el payload se encuentra en ICMP dentro de Data, en este caso como fue enviado desde Windows tiene 32 bytes y contiene datos arbitrarios ya que solo se utilizan para verificar que llegue la misma información en el reply. La principal diferencia es que en Linux el payload es de 56 bytes. 
![payload](Multimedia/12_payload.png)

**d)** TTL (Time to Live) es un mecanismo en el cual cada paquete tiene un valor que cada vez que hace un salto entre routers este le descuenta 1, esto se hace por que si se el paquete esta en un bucle en algún momento llegara a 0 y se destruira. En nuestra captura el valor es 128 para el request y 119 para el reply, el valor TTL de reply no es el original ya que este valor que recibimos es la resta luego de haber pasado por todos los routers necesarios para llegar a la pc.
![TTL](Multimedia/13_TTL.png)

**e)** 
![datoswireshark](Multimedia/14_bytes1.png) ![caja](Multimedia/14_bytes2.png)

# Inciso 2
##  ARP: de una IP a una dirección MAC
**a)** ARP es una solucion a la imposibilidad de usar el mapeo directo en direcciones fisicas
mas largas que una dirreccion Ipv4. Especilamente con direcciones Ethernet MAC que es 16 bits mas larga que una direccion Ipv4.
Todo dentro de la misma red fisica. Es dicutible en que capa ubicarla ya que su objetivo es mapear direciones IP que son de la capa 3
pero los mensajes no se encapsula en la capa sino que viajan en el entramado ethernet, que corresponde a la capa 2.

**b)**   ARP Request y ARP Reply

ARP Request : Es un paquete en el que se pregunta al host de una red que responda con la direccion hardware. Como aún no se conoce la direccion de esta, en el mensaje el
campo de la direccion fisica se llena con 0. Este paquete se envia a todos los dispositivos conectados a la misma red física.

ARP reply: Es un paquete que contiene tanto a la direccion Ipv4 como a la direccion fisica que se pidio
originalmente. Este paquete es enviado al equipo que solicito la direccion al principio.

**c)** ARP Cache

El ARP Cache es una memoria cache temporal donde se guardan las direccciones IP-to-hardware recientes con el objetivo
de optimizar el proceso para transmisiones susesivas, dado que, la transmision constante de request es caro y hace perder el tiempo.
Esto es algo especificado por el estadanr del software que es una obligacion tener.

**d)**

Primero busco en la memoria cache si recientemente se usado el IP-to-hardware asosiaciada a la IP que tengo de mi red local.
En caso de no encontrarse en el cache, lanzo una ARP Request con la IP que conozco y este me devuelve un ARP Reply con su MAC.
Luego guardo esta en el cache para un futuro uso.

**e)**

Sí,la MAC asociada al gateway coincide con la MAC destino que se vio anteriormente

**f)**

![Tabla rellena](Multimedia/tabla.png)

**a)**

El Request se envia a una dirección broadcast debido a que no conoce aún dispositivo en la red que tiene esa IP por lo que pregunta a toda la red
LAN para encontrarlo. En cambio, el reply es la respuesta del propietario de esta IP en la LAN que se envia a la MAC del equipo que hizo el request.
El Target MAC address en el request se encuentra relleno de ceros, porque no conoce la direccion MAC asociada a la IP que esta preguntando.

**b)**

El valor que tiene el campo Type es ARP(0x0806) y no tiene un encabezado IP. Como ARP no viaja dentro de la encapusalcion IP sino que viaja por la trama
ethernet podemos decir que este "vive" en el limite entre la capa 2 y capa 3.
**c)**

Al usar la opción A aparecieron 4 paquetes ARP Request y no se obtuvo ninguna reply. Al ser una IP inexistente no existe ningun dispositivo con esa IP en la LAN
por lo que nadie va a responder al broadcast tampoco se puede observar paquete ICMP porque al no obtener la reply el OS simplemente descarta los datos a enviar porque no es posible realizar un entramado ethernet. 

**d)**

Si aparecio nuevamente en el ARP Request como no se recibio una Reply al principio, no se guardo en el cache y el sistema vuelve a mandar la Request.
Por otro lado, la ventaja del uso de cache consiste en optimizar y acelerar el envio de paquetes, evitando saturar la red con broadcast frecuentes, aunque, en caso de 
quedar una ip vieja lo que podria ocurrir es que se siguiera mandando paquetes a esa ip antigua que el cache sigue guardando hasta que expire.
