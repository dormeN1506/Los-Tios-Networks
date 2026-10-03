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