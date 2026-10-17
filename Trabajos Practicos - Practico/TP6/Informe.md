# Trabajo Práctico N° 6: Redes de Computadoras

**Integrantes:**
* Arias, Daniel Andrés
* Garzón, Pablo
* Gutierrez, Patricio
* Fernández y Fernández, Sergio Ezequiel
* Loza Denardi, Gabriel Jeremías
* Rocatagliatta, Leandro Agustin
* Zambellini, Matías Manuel

---
## PARTE 1: Taller de armado y verificación de cables Cat5/Cat5e bajo estándar T568A/B

### Inciso 1

Para crimpar un cable de red **derecho** (directo) bajo la norma *T568A/B*, lo primordial es mantener el mismo código de colores en ambos extremos del cable. La norma más usada a nivel comercial y residencial es la **T568B** (la utilizada para este trabajo práctico).

Para poder armar el cable es necesario contar con:
* Cable de red de par trenzado (Cat5, Cat5e, Cat6).
* Dos conectores **RJ45**.
* Herramienta crimpadora.
* Pelacables.

Una vez que se cuenta con los materiales se deben seguir los siguientes pasos:
* **Pelar el cable:** Utilizar el pelacables para quitar entre **2 o 3 cm** de la cubierta exterior de plástico del cable de ambos extremos. Se debe tener cuidado de no cortar los hilos de cobre internos.
* **Desenredar y estirar los hilos:** Al tener los extremos ya pelados, se podrán observar 4 pares de hilos trenzados. Se debe separarlos, desenredarlos y estirarlos lo más derecho posible para que sea fácil ordenarlos (idealmente utilizar los dedos para este paso).
* **Ordernar los hilos según la norma elegida:** Según la norma elegida, se deben acomodar los hilos en cada extremo siguiendo un orden. Es sumamente importante que, para el tipo de cable **derecho**, en ambos extremos se debe respetar el mismo orden de los hilos:
    * *T568B:* De izquierda a derecha se debe colocar `blanco-naranja`, `naranja`, `blanco-verde`, `azul`, `blanco-azul`, `verde`, `blanco-marrón`, `marrón`.
    * *T568A:* De izquierda a derecha se debe colocar `blanco-verde`, `verde`, `blanco-naranja`, `azul`, `blanco-azul`, `naranja`, `blanco-marrón`, `marrón`.
* **Cortar a la medida:** Una vez que los cables estén en su orden específico y de forma plana, cortarlos de forma limpia y recta, dejando aproximadamente de **1.2 a 1.5 cm** de hilos expuestos desde el borde de la cubierta exterior.
* **Introducir los hilos en los conectores RJ45:** Con la pestaña de plástico del conector hacia abajo, se deben introducir todos los hilos firmemente hasta el fondo. Asegurarse que los hilos llegaron hasta el tope del conector y que la cubierta exterior del cable quede dentro del conector.
* **Crimpar el conector:** Introducir el conector *RJ45* en la ranura correspondiente de la crimpadora. Presionar los mangos con fuerza de forma constante. Al escuchar el clic es cuando los pines dorados pinchan los hilos y la pestaña de seguridad fija la cubierta del cable.
* **Repetir en el otro extremo:** Repetir los mismos pasos en el extremo que falta. Asegurarse de utilizar la misma orden que se usó en el primer extremo.

Si se cuenta con un tester, es posible verificar si el cable fue armado correctamente.

---

### Inciso 2

Siguiendo todos los pasos mencionados en el inciso anterior, logramos armar nuestro cable de red derecho bajo la norma **T568B** durante el horario de cursada. Al contar con testers probadores, pudimos afirmar que armamos el cable de forma correcta.

* **Prueba de funcionamiento de nuestro cable armado:**

![Funcionamiento de nuestro cable](Multimedia/Funcionamiento%20del%20cable%20armado%20(propio).gif)

---

### Incisos 3 y 4

Para este punto, intercambiamos nuestro cable de red con el del grupo **"Los Red(ondos)"** una única vez, adelantando que estaba armado de forma correcta.

* a) * **Cable armado por el grupo "Los Red(ondos) (1)":**
![Cable armado por el otro grupo (1)](Multimedia/Cable%20armado%20(Los%20Red(ondos)).jpeg)

**Cable armado por el grupo "Los Red(ondos) (2)":**
![Cable armado por el otro grupo (2)](Multimedia/Cable%20armado%20(Los%20Red(ondos))%20(2).jpeg)

Como puede observarse en la fotografía, todas las conexiones están hechas de forma correcta, los cables no son difíciles de identificar, el cable de red cuenta con un tamaño adecuado para usar fácilmente, los hilos dentro del conector también cuentan con un tamaño adecuado para lograr un buen crimpeado, llegar el tope y lograr buenas conexiones, y tal como se mencionó anteriormente, el cable funcionaba de manera correcta. Concluyendo así en una buena fabricación por parte del grupo con el que intercambiamos cables.

* b) **Verificación eléctrica del cable armado por el grupo "Los Red(ondos)":**

![Funcionamiento del cable armado por el otro grupo](Multimedia/Funcionamiento%20del%20cable%20armado%20(Los%20Red(ondos)).gif)

Tal como se mencionó, el cable del otro grupo estaba armado de forma correcta y funcionaba como tenía qué. En las siguientes partes de este trabajo, se utiliza este mismo cable para lograr un correcto envío y una correcta recepción de datos hacia y desde otro grupo mediante la utilización de un switch intermedio.

---

## PARTE 2: Equipamiento físico, verificación y utilización de equipos de red y generación de tráfico
