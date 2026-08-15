# Trabajo Práctico N° 1 Redes de Computadoras - Práctico

**Integrantes:**
* 
* 
* 
* 
* 
* 
* Zambellini, Matías Manuel

---
# Inciso 1

### Fundamentos de señales y comunicaciones

### Ondas electromagnéticas

Son ondas formadas por campos eléctricos y magnéticos que se propagan transportando energía e información. Se caracterizan principalmente por su amplitud, frecuencia y longitud de onda, relacionadas mediante C=λf.

### Modulación y demodulación

La modulación consiste en modificar una señal portadora, cambiando su amplitud, frecuencia o fase, para poder transmitir información por un medio. La demodulación es el proceso inverso: recuperar la información original desde la señal recibida.

### Señales de tiempo continuo

Son señales definidas para cualquier instante de tiempo. Esto significa que podemos conocer su valor en cualquier punto de (t). Generalmente se representan como (x(t)).

### Señales de tiempo discreto

Son señales definidas solamente en determinados instantes, normalmente obtenidos mediante el muestreo de una señal continua. Se representan como una secuencia (x[n]), donde cada valor corresponde a una muestra.

*a)* analizar el grafico

El gráfico representa una onda electromagnética periódica que se propaga en función de la distancia. El eje horizontal indica la distancia en milimetros y el eje vertical representa la amplitud de la señal. Los puntos ubicados en 60 mm y 120 mm se encuentran en la misma fase, por lo que permiten calcular la longitud de onda. Además, se observa que la amplitud disminuye a medida que aumenta la distancia.

*b)*

      λ = 120mm − 60mm = 60mm = 0,06m
      C=  3 x 10^8m/s
      C=λf
      f = C/λ = 3 x 10^8/0,06 = 5 x 10^9 = 5GHz
      
*c)* Teniendo en cuenta lo calculado anteriormente vemos que tiene una longitud de onda de 0,06m esto significa que en el rango del espectro electromagnetico se encontraria en la region de ondas de radio y la banda segun ITU seria SHF(Super High Frequency o frecuencia superalta), denominada banda 10, que comprende las frecuencias entre 3 GHz y 30 GHz.     
      
*d)* En la banda SHF operan dispositivos como routers, puntos de acceso y adaptadores Wi-Fi, además de enlaces de microondas, radares y algunos sistemas satelitales.
Un ejemplo adecuado para nuestro caso es un router o punto de acceso Wi‑Fi que funciona en 5 GHz. 

*e)* La línea roja representa la atenuacion de la señal. A medida que la onda recorre una mayor distancia, pierde energía y disminuye su amplitud, por lo que llega más débil al receptor.

*f)* Justamente el caso de la atenuacion en señales wi-fi es muy comun y se nota en la vida cotidiana al alejarse del router y observar que empeora la señal recibida y la conexión puede volverse más lenta e inestable.

*g)* 
  i) si, en las transmisiones de telefonía celular la señal empeora al alejarnos de la antena y al atravesar edificios o paredes.
  ii) si, las transmisiones por cable coaxial la señal pierde potencia mientras recorre el cable debido principalmente a la resistencia de los conductores y a perdidas en el material aislante.
  iii) no es tan considerable la atenuacion en la fibra optica debido a que se utiliza la luz, pero si los cables no se encuentran instalados de la manera correcta puede presentar atenuacion.
  # Inciso 3
Los diversos motivos por los cuales se la transmisión inalámbrica de una señalescalonada no seria conveniente son los siguientes:  
* Señalizacion: En el caso del uso de una señalizacion digital, buscando una ventaja economica termina provocando un mayor efecto de la atunuacion en señales digitales.
* Atenuacion: Como se busca usar un medio no guiado vamos a tener una funcion mas compleja de la distancia y terminar dependiendo de las condiciones atmosféricas.Ademas, como se menciono anteriormente, las señales digitales sufren mas la atenuacino que las analogicas.
* Distorsión de retardo: Esta distorsión,producida por la retardo variable en las componetes de la señal,es particularmente critica en la transmision de datos digitales limitando la velocidad de transmisión máxima.Ademas, se usan técnicas de ecualización para aterunar el efecto.
* Ruido impulsivo: Ruido no continuo constituido por picos irregualares de corta duración que es uno de los principales errores en la comunicación digital de datos, un pico de energía de 0.01 s podría corromper hasta 560 bits si se transmiten a 56kbps.  

#### Analisís de señal
*a)* La técnica de modulación que se representa en la imagen es la técnica de modulación por desplazamiento de fase o PSK.    

*b)* Onda modularizada : ![OndaModularizada](Multimedia/OndaInciso3.png)

*c)* El principio de la modulación por desplazamiento de fase (PSK) consiste en provocar la variación en una de la características físicas de la señal portadora para la representar datos digitales. Otras técnicas de modulación que siguen el mismo principio son la modulación por desplazamiento por amplitud (ASK) y la modulación desplazamiento por frecuencía (FSK).

*d)* El Bit Error Rate (BER) es una métrica que cuantifica la proporción de bits que se reciben de forma incorrecta respecto al total de bits transmitidos en un determinado periodo de tiempo. En terminos de prestaciones, la modulación PSK es la mejor en cuanto al BER, ya que es mas robusta y  tan sensible al ruido como la ASK y FSK.



# Inciso 4

*c)* El router opera en el canal de los 2.4 GHz. A esa frecuencia, opera en la región del espectro denominada Ultraalta frecuencia (Ultra High Frequency - UHF); utilizadas comunmente en servicios de comunicación en tierra, telefonía celular y comunicaciones militares. Opera en la banda de las microondas, donde las longitudes de onda abarcan aproximadamente desde 1 m hasta 100 mm.

*g)* Al realizar las conexiones necesarias se puede observar que las conexiones entre cada computadora al router inalámbrico y entre las computadoras entre sí fue realizada correctamente. Se transmiten 4 paquetes desde la PC a la Notebook 1 (mediante el comando `ping`) y cada uno llega de forma pertinente, sin pérdidas de información. De la misma forma, se comprobó el camino que realizan los paquetes para llegar a su destino (mediante el comando `tracert`).
* IP Config de la PC: ![IPConfigPC](Multimedia/IPConfig%20PC.JPG)
* IP Config de la Notebook 1: ![IPConfigNotebook1](Multimedia/IPConfig%20Notebook.JPG)
* Ping y Tracer entre las computadoras: ![Ping_Tracer](Multimedia/ping%20y%20tracer%20PC.JPG)

*h)* Al agregar la nueva Notebook 2 para esta parte y hacer la conexión a la señal SSID configurada anteriormente, se puede observar que estando cerca del límite del rango de la señal se logra la correcta conexión (aunque la señal llegue de forma pobre). Para probar la reacción, se mandaron paquetes desde la PC hacia la Notebook 2 (mediante el comando `ping`) y todos lograron al destino sin ninguna pérdida. Al quitar la Notebook 2 del rango de la señal e intentar mandar los paquetes desde la PC, directamente no se logró el objetivo y hubo una pérdida total de la información ya que se excedió el tiempo de respuesta estipulado (`Requested timed out`).
* Notebook 2 en rango (límite) de la señal: ![Notebook2EnRango](Multimedia/Notebook%202%20en%20rango%20de%20señal.JPG)
* Notebook 2 fuera de rango de la señal: ![Notebook2FueraDeRango](Multimedia/Notebook%202%20fuera%20de%20rango%20de%20señal.JPG)
