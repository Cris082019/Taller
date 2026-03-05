# Parcial

<img width="1511" height="262" alt="image" src="https://github.com/user-attachments/assets/bc927545-ff02-4f94-aa70-98d9415e1e08" />

<img width="1283" height="125" alt="image" src="https://github.com/user-attachments/assets/77869575-9840-4e9c-acc5-36458d740171" />
La diferencia radica en la constancia del tiempo de los datos


**Latencia:** Es el tiempo total que tarda un paquete de datos en viajar desde el origen hasta el destino. Se mide generalmente en milisegundos (ms). Es el "retraso" puro.<br>

**Jitter:** Es la variación en el tiempo de llegada de los paquetes (la variabilidad de la latencia). Si un paquete tarda 50ms y el siguiente 80ms, ese cambio de ritmo es el jitter.<br>

**¿Cuál tiene un impacto más negativo en VoIP?**<br>
El **Jitter** suele ser más perjudicial.<br>

¿Por qué?
Aunque una latencia alta es molesta (causa ese silencio incómodo donde ambos hablan a la vez), el cerebro humano puede adaptarse a un retraso constante. Sin embargo, el jitter causa distorsión, audio entrecortado o robótico. Como los paquetes de voz deben reensamblarse en orden y a un ritmo constante para que el sonido sea fluido, si llegan a ritmos distintos, el procesador no puede reconstruir la señal correctamente, provocando una pérdida de calidad inmediata y frustrante.

<img width="1278" height="248" alt="image" src="https://github.com/user-attachments/assets/06145881-6e96-42bc-9852-31585283ece8" />

**1.** Mayor eficiencia en términos de Throughput: **UDP**<br>
UDP es más eficiente para mover grandes volúmenes de datos rápidamente.<br>

**2.** Mayor control de la pérdida de paquetes: **TCP**<br>
TCP es el protocolo "fiable" por excelencia.<br><br>
Si un paquete se pierde, el receptor lo nota por el número de secuencia y no envía el "ACK".<br>
TCP entonces activa mecanismos de retransmisión para recuperar ese dato perdido. UDP, al carecer de estos campos, simplemente ignora si algo se perdió en el camino.<br><br>

<img width="1387" height="222" alt="image" src="https://github.com/user-attachments/assets/914fab82-bab6-42af-af64-66301d75b75e" />
<img width="595" height="1074" alt="image" src="https://github.com/user-attachments/assets/12241b59-0b89-41c3-bafe-5f8ebc93a359" />

El protocolo que llena esta tabla es el **ARP (Address Resolution Protocol)** o Protocolo de Resolución de Direcciones.<br><br>
**Función principal en una red local**<br>
Su función es actuar como un "traductor" entre la Capa de Red (Capa 3) y la Capa de Enlace de Datos (Capa 2).<br>
Cuando un equipo conoce la dirección IP de destino pero no su dirección física (MAC), envía una consulta ARP.<br>
El protocolo permite que los datos lleguen al hardware correcto dentro de la misma red local (LAN).<br>
Como ves en tu imagen, la tabla mapea cada IP (ej. 192.168.238.254) con su correspondiente dirección física (ej. 00-50-56-ea-76-ae).<br><br>
**Relación con la estructura de una trama Ethernet**<br>
Para que la información viaje por el cable o el aire, se debe encapsular en una trama Ethernet. Aquí es donde ARP es vital:<br><br>
**El destino físico:** Una trama Ethernet requiere obligatoriamente una MAC de destino en su cabecera para ser entregada por el Switch.<br>
**La construcción de la trama:** Sin el protocolo ARP, el equipo emisor dejaría el campo "Destination MAC" vacío y la trama no podría enviarse.<br>
**Encapsulamiento:** Una vez que ARP obtiene la dirección física y la guarda en la tabla (como se muestra en tu CMD), el sistema toma esa dirección y la coloca en el encabezado de la trama Ethernet, permitiendo que el paquete IP viaje de forma segura hacia el equipo correcto.

<img width="1387" height="119" alt="image" src="https://github.com/user-attachments/assets/258777f2-0fd4-4e5f-a25e-db669dd917ac" />

**Diferencias clave: SNMPv2c vs. SNMPv3**<br>
**SNMPv2c**<br>
***Seguridad:*** Básica. Usa una "cadena de comunidad" (community string) que viaja en texto plano, lo que es vulnerable a intercepciones.<br>
***Mensajes:*** Se limita principalmente a mensajes simples. No garantiza la recepción de notificaciones.<br><br>

**SNMPv3**<br>
***Segurida:*** Avanzada. Introduce un modelo de seguridad basado en el usuario (USM) que permite autenticación y cifrado de los datos.<br>
***Mensajes:*** Introduce mensajes "Inform". A diferencia del Trap común, el mensaje Inform requiere una confirmación de recepción, asegurando que el administrador recibió el evento.<br><br>

Mientras que SNMPv2c es rápido pero inseguro, SNMPv3 es el estándar actual porque protege la gestión de la red mediante criptografía y añade fiabilidad a las notificaciones.<br><br>

<img width="1379" height="189" alt="image" src="https://github.com/user-attachments/assets/7590ef87-29c3-4397-8ab7-acc844559951" />

**OID y su relación con la MIB**

**OID (Object Identifier):** Es un nombre numérico único (como 1.3.6.1.2...) que identifica de forma específica un objeto o variable dentro de un dispositivo de red.<br>
**Relación con la MIB:** La MIB (Management Information Base) es la base de datos jerárquica que organiza todos estos objetos. Imagina que la MIB es un "mapa" o "biblioteca" y el OID es la "coordenada" o el "código de barras" exacto para encontrar un dato dentro de ella.

**Operación para consultar bytes recibidos**<br>
El administrador debe utilizar la operación Get (SNMP Get).

**¿Por qué Get?** Porque es la operación diseñada para que el administrador solicite activamente el valor actual de una variable específica (en este caso, el contador de bytes) desde el agente del dispositivo.

**¿Por qué no usar un Trap?** Un Trap es una alerta no solicitada que envía el dispositivo solo cuando ocurre un evento crítico o inusual (ej. una interfaz se apaga o un error de energía).

No es adecuado para consultar estadísticas rutinarias como el conteo de bytes, ya que saturaría la red enviando alertas constantes por un dato que cambia cada segundo.


