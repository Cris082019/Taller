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



