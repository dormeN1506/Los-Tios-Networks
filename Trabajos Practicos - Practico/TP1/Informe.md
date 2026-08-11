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

# Inciso 4

*c)* El router opera en el canal de los 2.4 GHz. A esa frecuencia, opera en la región del espectro denominada Ultraalta frecuencia (Ultra High Frequency - UHF); utilizadas comunmente en servicios de comunicación en tierra, telefonía celular y comunicaciones militares. Opera en la banda de las microondas, donde las longitudes de onda abarcan aproximadamente desde 1 m hasta 100 mm.

*g)* Al realizar las conexiones necesarias se puede observar que las conexiones entre cada computadora al router inalámbrico y entre las computadoras entre sí fue realizada correctamente. Se transmiten 4 paquetes desde la PC a la Notebook 1 (mediante el comando `ping`) y cada uno llega de forma pertinente, sin pérdidas de información. De la misma forma, se comprobó el camino que realizan los paquetes para llegar a su destino (mediante el comando `tracert`).
* IP Config de la PC: ![IPConfigPC](Multimedia/IPConfig%20PC.JPG)
* IP Config de la Notebook 1: ![IPConfigNotebook1](Multimedia/IPConfig%20Notebook.JPG)
* Ping y Tracer entre las computadoras: ![Ping_Tracer](Multimedia/ping%20y%20tracer%20PC.JPG)

*h)* Al agregar la nueva Notebook 2 para esta parte y hacer la conexión a la señal SSID configurada anteriormente, se puede observar que estando cerca del límite del rango de la señal se logra la correcta conexión (aunque la señal llegue de forma pobre). Para probar la reacción, se mandaron paquetes desde la PC hacia la Notebook 2 (mediante el comando `ping`) y todos lograron al destino sin ninguna pérdida. Al quitar la Notebook 2 del rango de la señal e intentar mandar los paquetes desde la PC, directamente no se logró el objetivo y hubo una pérdida total de la información ya que se excedió el tiempo de respuesta estipulado (`Requested timed out`).
* Notebook 2 en rango (límite) de la señal: ![Notebook2EnRango](Multimedia/Notebook%202%20en%20rango%20de%20señal.JPG)
* Notebook 2 fuera de rango de la señal: ![Notebook2FueraDeRango](Multimedia/Notebook%202%20fuera%20de%20rango%20de%20señal.JPG)