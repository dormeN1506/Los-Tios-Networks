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

