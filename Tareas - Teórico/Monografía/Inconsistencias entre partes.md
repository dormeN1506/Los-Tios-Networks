# Inconsistencias entre las partes de la monografía

Revisión cruzada del 9/11/2026 sobre las versiones que están en el repositorio:

| Parte | Archivo revisado |
|---|---|
| 1 | `Parte 1/Parte 1 (Introducción, metodología e infraestructura física).docx` |
| 2 | `Parte 2/Parte2.docx` |
| 3 | `Parte 3/Seccion_3_monogafia.docx` |
| 4 | `Parte 4/4 Estructuras de servidores (corregido).docx` |
| 6 y 7 | Las que se suben junto con este documento |

La Parte 5 todavía no está en el repositorio; al final hay una lista de lo que conviene revisar cuando se suba.

Cada punto indica **dónde** está el problema, **qué dice hoy** y **qué se recomienda poner**. Los textos sugeridos son una propuesta: cada autor puede adaptarlos a su redacción.

## Decisiones ya tomadas

- **FW2 será MikroTik.** Las Partes 6 y 7 ya están escritas así.
- **Red interna de Proxmox:** la Parte 4 es la correcta, no la 3. Ver el punto 4, porque la Parte 4 cambió después de esa decisión.
- **SW1 a SW4 se reutilizan como switches de acceso**, a partir de lo que relevó la Parte 2. Las Partes 6 y 7 ya están ajustadas.

## Resumen

| N.º | Partes | Tema | Qué hay que hacer |
|---|---|---|---|
| 1 | 1, 2 y 4 | Direcciones IP reales | Decidir un criterio común y aplicarlo |
| 2 | 1 | Wi-Fi descrito como «invitados/alumnos» con NAT | Corregir la Parte 1 según las Partes 2 y 3 |
| 3 | 1 | Switches «genéricos» y «no administrables» | Corregir la Parte 1 según la Parte 2 |
| 4 | 3 y 4 | Red interna de Proxmox: ¿VLAN o red dedicada? | Confirmar el dato y ajustar las Partes 3 y 4 |
| 5 | 1 | Promete mejorar el rendimiento de los clústeres | Ajustar el objetivo |
| 6 | 2 | El último párrafo está cortado | Completarlo |
| 7 | 4 | Cita la «Figura 2» de la sección 1.4 | Actualizar cuando se numere la Parte 1 |
| 8 | Todas | Formato de página, títulos, figuras, tablas y bibliografía | Unificar al armar el documento |
| 9 | 5 | Todavía no se subió | Revisar cuando esté |

---

## 1. Direcciones IP reales (Partes 1, 2 y 4)

**Consigna del grupo:** «No debemos publicar direcciones IP reales ni información sensible de la infraestructura, como pidió el encargado».

**Problema:** cada parte usa un criterio distinto.

- **Parte 1:** oculta el último octeto (`172.16.48.X`, `10.0.1.X`, …), pero el prefijo de red sigue siendo real. También aparece dentro de dos figuras.
- **Parte 2:** publica las redes completas (tabla 2.2 y figura 2.2) y oculta solo el bloque público.
- **Parte 4:** oculta el último octeto, igual que la Parte 1.
- **Parte 6:** usa un plan con rangos inventados (tabla 6.4).

**Recomendación:** no publicar ningún rango real, ni siquiera parcial. Alcanza con indicar la función de cada red y, si hace falta, su tamaño (/24, /29). Es lo mismo que la Parte 2 ya hace con el bloque público.

Si el grupo decide que las redes privadas sí se pueden publicar, hay que usar el mismo criterio en todas las partes. La Parte 6 seguiría con rangos inventados, porque es una propuesta.

### Cambios en la Parte 1

| Dónde | Dice hoy | Poner |
|---|---|---|
| 1.3, primer párrafo | `(IP Gateway: 172.24.0.X)` y `(IP: 172.24.0.X)` | Borrar los dos paréntesis |
| 1.3, tercer párrafo | `(salida a través de la IP 200.16.16.X)` | Borrar el paréntesis |
| 1.3, «Distribución de red interna», primer párrafo | `SW1 (172.16.48.X), SW2 (172.16.48.X), SW3 (172.16.48.X) y SW4 (172.16.48.X)` | Ver el punto 3, que reescribe esa oración |
| 1.3, viñeta de la red de invitados y tabla de equipos | `192.168.0.X/24`, `172.16.48.X` y `DHCP 192.168.0.X` | Ver el punto 2, que reescribe la viñeta |
| 1.4, viñeta «Clúster Yaku» | `red interna dedicada (10.0.1.X)` | `red interna dedicada` |
| 1.4, «Redes especiales», primer párrafo | `Red SAN de 10 Gbps (10.90.0.X)` | `Red SAN de 10 Gbps` |
| 1.4, «Redes especiales», segundo párrafo | `en el segmento 10.20.0.X` | `en un segmento propio` |
| 1.4, «Redes especiales», tercer párrafo | `red principal (172.16.48.X)` | `red principal` |
| 1.4, tabla de servidores | `(10.0.1.X)`, `(172.16.48.X)` y `(10.20.0.X)` | Borrar los paréntesis |
| Figura de topología física (`Parte 2 cap1 (mejorada).PNG`) | Rótulos `[Red privada: 172.16.48.X]` | `[Red privada]` o borrar los rótulos |
| Figura de servidores (`Parte 3 cap 1 (mejorada).PNG`) | `10.0.1.X`, `10.90.0.X`, `10.20.0.X` y `172.16.48.X` | Borrar los rótulos o cambiarlos por el nombre de la red (red de cálculo, SAN, heartbeat, red principal) |

### Cambios en la Parte 2

| Dónde | Dice hoy | Poner |
|---|---|---|
| 2.3, tabla 2.2, columna «Red» | Redes completas (`172.16.48.0/24`, `192.168.81.0/24`, etc.) | Solo el tamaño: `/24`, `/22`, `/29`. Cambiar el título de la columna a «Tamaño» |
| 2.3, último párrafo | `192.168.85.0/24 para Android y 192.168.86.0/24 para iOS` | `dos subredes /24, una para Android y otra para iOS` |
| 2.5, segundo párrafo | `(192.168.85.0/24)` y `(192.168.86.0/24)` | Borrar los paréntesis |
| Figura 2.2 | Direcciones dentro de los recuadros | Dejar solo el tamaño y la VLAN, por ejemplo `/24 · VLAN 81` |

Los ID de VLAN (1, 2, 81, 381 y 900) pueden quedar: no son direcciones y la Parte 6 los cita.

### Cambios en la Parte 4

| Dónde | Dice hoy | Poner |
|---|---|---|
| 4.1.1 | `red principal (172.16.48.X)` y `red interna dedicada (10.0.1.X)` | Borrar los paréntesis |
| 4.4, las tres viñetas | `Red Heartbeat / Clúster (10.20.0.X)`, `Red SAN de Base de Datos (10.90.0.X)` y `Red de Servicios (172.16.48.X)` | Borrar los paréntesis |

El `8.8.8.8` de 4.4.1 es el resolutor público de Google, no un dato del laboratorio, así que puede quedar.

---

## 2. Wi-Fi: la Parte 1 describe una red de invitados con NAT

**Dónde:**

- Parte 1, sección 1.3: la viñeta «Red de invitados/alumnos».
- Parte 1, tabla de equipos: la fila «Puntos de Acceso».

**Problema:**

- **Parte 1:** dice que la red de invitados usa `192.168.0.X/24` y que sale a la red interna por NAT.
- **Parte 2 (2.3 y 2.5):** se basa en la configuración del router. Muestra que las redes para teléfonos son dos subredes, una para Android y otra para iOS. Aclara que la otra subred mencionada en la entrevista era un error y que el NAT solo fue una propuesta.
- **Parte 3 (3.2):** también dice que ese NAT no estaba implementado.
- **Parte 6:** ya usa la versión de la Parte 2.

**Dice hoy (viñeta):**

> ***Red de invitados/alumnos:*** Asigna direccionamiento privado en el rango 192.168.0.X/24 mediante DHCP. Para evitar el agotamiento de direcciones en el segmento principal de servidores, el tráfico de esta red inalámbrica atraviesa una regla de NAT (Traducción de Direcciones de Red) en el MikroTik, saliendo hacia la red interna a través de una única dirección IP (172.16.48.X).

**Poner:**

> ***Redes de dispositivos móviles:*** dos subredes privadas propias, una para Android y otra para iOS, asignadas por DHCP. Se separaron del segmento principal para evitar que los teléfonos consumieran las direcciones destinadas a los equipos de trabajo. El acceso desde estas redes a los servicios internos mediante NAT se mencionó como posibilidad, pero no está implementado (secciones 2.5 y 3.2).

**Tabla de equipos, fila «Puntos de Acceso (Wi-Fi)»:**

- **Columna «Marca/Modelo»:** `Ubiquiti` → `Ubiquiti (3 UAP y 1 UAP-AC-PRO)`. Son los modelos que da la Parte 2 (2.5).
- **Columna «Función»:** `… para redes "eduroam" e invitados (DHCP 192.168.0.X).` → `… para eduroam y las redes de dispositivos móviles.`

---

## 3. Parte 1: switches «genéricos» y «no administrables»

**Dónde:** Parte 1, sección 1.3 (primer párrafo de «Distribución de red interna» y la tabla de equipos) y sección 1.5 (tercer párrafo).

**Problema:**

- **Qué dice la Parte 1:** llama «genéricos» a los switches de distribución. En 1.5 dice que la cascada de switches TP-Link no es administrable y que eso impide usar VLAN.
- **Qué identifica la Parte 2 (2.1):**
  - router MikroTik CCR2116-12G-4S+;
  - switches de distribución MikroTik de la familia 326, administrables y conectados por fibra;
  - un TP-Link T2600G-18TS;
  - un Cisco SG110-24 para los nodos de Yaku;
  - un TP-Link TL-SX1008 para la SAN.
- **VLAN:** la Parte 2 muestra además que la VLAN 81 de cámaras ya existe, así que segmentar con VLAN no es imposible.
- **Lo que sí es no administrable:** solo los micro-switches TP-Link de 5 puertos que cuelgan de la distribución.

**1.3, primer párrafo de «Distribución de red interna».** Dice hoy:

> A partir del MikroTik, el cableado se extiende hacia una cadena de conmutadores de distribución configurados con direccionamiento estático: SW1 (172.16.48.X), SW2 (172.16.48.X), SW3 (172.16.48.X) y SW4 (172.16.48.X).

Poner (resuelve también el punto 1):

> A partir del MikroTik, enlaces de fibra óptica llegan a los conmutadores de distribución SW1, SW3 y SW4, switches MikroTik de la familia 326 con direcciones fijas en la red principal; SW2 se conecta en cascada detrás de SW1.

**1.3, segundo párrafo del mismo apartado.** Dice «De estos nodos derivan conexiones hacia micro-switches de acceso no administrables…». Está bien y puede quedar como está.

**1.3, tabla de equipos:**

| Fila | Columna «Marca/Modelo» hoy | Poner |
|---|---|---|
| Enrutador/Borde | `MikroTik (16 cores)` | `MikroTik CCR2116-12G-4S+ (16 núcleos)` |
| Conmutadores (Distribución) | `Switches genéricos` | `MikroTik (familia 326)` |
| Conmutador SAN | `Genérico (10 Gbps)` | `TP-Link TL-SX1008 (10 Gbps)` |

Opcional: agregar la fila «Conmutador del clúster Yaku | Cisco SG110-24 | 1 | Red interna exclusiva entre el máster Yaku y sus nodos».

**1.3, primer párrafo de «Infraestructura de Borde».** Dice `router MikroTik equipado con 16 núcleos de procesamiento`. Poner `router MikroTik CCR2116-12G-4S+, equipado con 16 núcleos de procesamiento`.

**1.5, tercer párrafo.** Dice hoy:

> Por otro lado, la capa de distribución presenta serias debilidades de hardware. La utilización de *switches* de tipo hogareño o Pyme (TP-Link) interconectados en cascada para brindar servicio a las terminales y cámaras de seguridad constituye un riesgo latente. Estos equipos no solo agregan latencia y puntos únicos de falla (SPOF), sino que, al no ser administrables, imposibilitan la segregación del tráfico mediante redes locales virtuales (VLANs).

Poner:

> Por otro lado, la capa de distribución presenta debilidades. Los switches de distribución (MikroTik de la familia 326) son administrables, pero parte de ellos está conectada en cascada (SW1 y SW2), y de ellos cuelgan micro-switches TP-Link de tipo hogareño que brindan servicio a terminales y cámaras. La cascada agrega latencia y puntos únicos de falla (SPOF), y los micro-switches, al no ser administrables, no pueden participar de la segregación del tráfico mediante VLAN.

---

## 4. Red interna de Proxmox: ¿VLAN o red dedicada? (Partes 3 y 4)

**Qué pasó:**

1. **Primera versión de la Parte 4:** decía que la red interna de Proxmox/Swarm era «una VLAN».
2. **Parte 3 (3.2):** dice que pasar Proxmox a una VLAN era «una reorganización pendiente».
3. **Decisión del grupo:** la Parte 4 es la correcta.
4. **Versión corregida de la Parte 4 (4.4):** unifica esa red con la heartbeat en una sola «Red Heartbeat / Clúster», pero ya no dice que sea una VLAN.
5. **Figura de servidores de la Parte 1:** muestra esa red sobre un switch propio.

**Qué falta:** que el autor de la Parte 4 confirme cuál es el dato correcto. La Parte 6 ya está redactada de forma compatible con las dos opciones: «ya existe como red propia».

### Si es una VLAN (la decisión del grupo)

**Parte 4, 4.4, primera viñeta.** Agregar que es una VLAN:

> **Red Heartbeat / Clúster:** red privada de control, implementada como una VLAN propia, que conecta internamente los nodos de Proxmox. …

**Parte 3, 3.2, final del segundo párrafo.** Dice hoy:

> La separación de estas últimas utiliza interfaces y switches dedicados; la presencia de un rango propio no basta para clasificarlas como VLAN.

Poner:

> Las de cálculo y almacenamiento utilizan interfaces y switches dedicados, por lo que la presencia de un rango propio no basta para clasificarlas como VLAN; la red de clúster de Proxmox, en cambio, funciona en una VLAN propia (sección 4.4).

**Parte 3, 3.2, tercer párrafo.** Dice hoy:

> Durante el relevamiento se mencionó la propuesta de utilizar un mismo switch para separar mediante VLAN la comunicación interna de Proxmox y el tráfico de cámaras. La VLAN de cámaras ya existía, mientras que el traslado de Proxmox se planteó como una reorganización pendiente. Con esa distribución, ambos tráficos compartirían el equipo físico, pero permanecerían separados en capa 2. Para comunicarlos harían falta encaminamiento y permisos de acceso.

Poner:

> Durante el relevamiento se mencionó la propuesta de que la red de clúster de Proxmox y el tráfico de cámaras compartan un mismo switch. Ambos ya funcionan en VLAN propias (secciones 2.2 y 4.4), por lo que compartirían el equipo físico, pero permanecerían separados en capa 2. Para comunicarlos harían falta encaminamiento y permisos de acceso.

### Si es una red sobre un switch dedicado

La Parte 3 ya está bien y no hay que cambiar nada.

---

## 5. Parte 1: el objetivo promete mejorar el rendimiento de los clústeres

**Dónde:** Parte 1, sección 1.1, última oración del tercer párrafo.

**Problema:** las Partes 6 y 7 no proponen cambios en los clústeres de cálculo. La síntesis 6.7 dice: «La propuesta no reemplaza la infraestructura de cómputo».

**Dice hoy:**

> …se propondrá un rediseño integral orientado a optimizar la segmentación, robustecer la seguridad mediante firewalls dedicados y mejorar el rendimiento de los clústeres de cálculo.

**Poner:**

> …se propondrá un rediseño integral orientado a optimizar la segmentación, robustecer la seguridad mediante firewalls dedicados y mejorar la disponibilidad de los servicios.

---

## 6. Parte 2: el último párrafo está cortado

**Dónde:** Parte 2, sección 2.8, último párrafo. Termina en «…las siguientes secciones pueden profundizar en el encaminamiento, los servicios y las».

**Poner, por ejemplo:**

> …las siguientes secciones pueden profundizar en el encaminamiento, los servicios y las propuestas de mejora.

---

## 7. Parte 4: referencia a la «Figura 2»

**Dónde:** Parte 4, sección 4.5.

**Problema:** dice «pueden visualizarse en detalle en la **Figura 2** (referirse a la *Sección 1.4* …)». Hoy las figuras de la Parte 1 están sin numerar (ver el punto 8).

**Poner,** cuando la Parte 1 numere sus figuras:

> …pueden visualizarse en detalle en la figura 1.2 (sección 1.4).

---

## 8. Formato (para la unificación final)

- **Tamaño de página:** las Partes 1 y 2 están en Carta; las 3, 4, 6 y 7, en A4. Pasar todo a A4.
- **Títulos:** conviene usar los estilos de título de Word (Título 1, 2 y 3) en todas las partes, así el índice automático los toma. Hoy hay títulos que son párrafos en negrita: 1.1 y 1.2 de la Parte 1, y todos los de la Parte 4.
- **Numeración de los títulos:** unificar el formato «N.M Título». Las Partes 2 y 3 terminan el número con punto («2.1.», «3.1.»).
- **Subsección sin número en la Parte 3:** «Publicación de servicios y traducción de direcciones», entre 3.4 y 3.5. Numerarla.
- **Figuras de la Parte 1:** las tres dicen «Figura [x]». Numerarlas 1.1, 1.2 y 1.3.
- **Epígrafes de figura:** las Partes 1, 4, 6 y 7 usan «Figura N.M: texto»; las 2 y 3, «Figura N.M. texto». Elegir uno.
- **Tablas de la Parte 1:** las dos no tienen título. Agregar, arriba y en negrita como en el resto: «Tabla 1.1. Equipamiento de red relevado.» y «Tabla 1.2. Clústeres y servidores relevados.».
- **Nombre del servicio de DNS:** la Parte 4 escribe «CloudNS»; el nombre del servicio es «ClouDNS», como en la Parte 6.
- **Bibliografía:** las Partes 3 y 7 tienen lista propia; las 1, 2, 4 y 6, no. Al unificar, armar una sola lista en formato APA al final. Conviene que todas citen la charla con el personal del laboratorio, como hace la Parte 3. La Parte 2 debería citar además el documento *Red LH* (2022) y las capturas de la configuración.

---

## 9. Parte 5 (todavía no está en el repositorio)

Cuando se suba, conviene revisar que:

- **Hallazgos:** coincidan con la tabla 6.1 y con la columna «Situación actual» de la tabla 6.5. La Parte 6 cita la sección 5 como diagnóstico de seguridad.
- **IPMI:** figure como la vulnerabilidad más crítica, como dicen 1.5, 6.4 y 7.5.2.
- **Firewall del MikroTik:** sus limitaciones coincidan con 6.2 (un solo equipo con todos los roles).
- **Wi-Fi:** use la misma descripción que las Partes 2 y 6 (redes de teléfonos Android e iOS, sin NAT hacia la red interna).
- **Switches:** no diga que los switches de distribución impiden usar VLAN (ver el punto 3).
- **Direcciones IP:** respete el criterio que se decida en el punto 1.

---

## Referencia: qué cambió en las Partes 6 y 7

Para que el resto del grupo sepa qué se ajustó a partir de las otras partes:

- **FW2:** MikroTik CCR2004, con detección de intrusiones (Suricata) en lugar de prevención. La diversidad de fabricante queda como mejora futura.
- **FW1:** es el CCR2116-12G-4S+ actual, el modelo que da la Parte 2.
- **Conmutación:**
  - SW1 a SW4 se reutilizan como switches de acceso; se elimina la cascada y se retiran los micro-switches TP-Link.
  - Se compran dos núcleos con puertos de fibra (CRS309), un switch para los servidores y un switch para la red de gestión.
  - El repuesto de la SAN es un TL-SX1008 igual al actual.
- **Wi-Fi:** las redes de teléfonos (Android e iOS) pasan a una VLAN propia, sin acceso a los servidores.
- **Red de clúster de Proxmox (heartbeat):** es una sola red, como en la Parte 4 corregida, y se mantiene sin puerta de enlace.
- **Direcciones:** la tabla 6.4 usa rangos inventados (RFC 1918), sin datos de la red real.
- **Presupuesto:** fase A USD 4.504,07; total USD 9.563,72 (a $1.570 por dólar).
