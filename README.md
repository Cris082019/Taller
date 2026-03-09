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


<img width="1051" height="432" alt="image" src="https://github.com/user-attachments/assets/fdd33841-b13f-4330-9247-2ab184ab5297" /><br>

Basándonos en la captura, los campos de la cabecera Ethernet II son:

🔴 **Destino (aa:bb:cc:dd:ee:ff):** Es la dirección MAC del dispositivo receptor (o del siguiente salto, como un router) en la red local. Indica a qué hardware específico va dirigida la trama.<br>
🔴 **Origen (00:11:22:33:44:55):** Es la dirección MAC de la tarjeta de red (NIC) del dispositivo que generó la trama.<br>
🔴 **Tipo (0x0800):** Este campo (EtherType) indica qué protocolo de la capa superior (Capa 3) está encapsulado dentro de los datos de la trama.

***¿Qué significa el valor 0x0800 en el campo "Tipo"?***<br>
El valor 0x0800 es el código estándar para IPv4 (Internet Protocol version 4).<br>
🔵 Su importancia: Le indica al receptor que, tras procesar la cabecera Ethernet, debe pasar el contenido restante a la pila del protocolo IP para su lectura. Si fuera, por ejemplo, 0x86DD, indicaría que el contenido es IPv6.

<img width="960" height="88" alt="image" src="https://github.com/user-attachments/assets/8454081c-2627-49e7-809c-4b8932e96018" />

**1. Campo:** Protocolo<br>
Este campo indica cuál es el protocolo de la Capa de Transporte (Capa 4) que está encapsulado dentro del paquete IP.

Significado en tu caso: El valor 6 corresponde específicamente a TCP.

Función: Al igual que el campo "Tipo" en Ethernet, el campo "Protocolo" le dice al receptor: "Oye, ya terminé de procesar la capa de red; ahora entrega estos datos al módulo de TCP". Si el valor fuera 17, se entregaría a UDP.

**2. Campo:** TTL (Time To Live / Tiempo de Vida)<br>
El TTL es un contador que limita la vida de un paquete en la red para evitar que circule infinitamente.

Funcionamiento: Cada vez que el paquete atraviesa un router (un salto), este le resta 1 al valor del TTL.

Significado en tu caso: Tu captura muestra un TTL de 128. Esto sugiere que el paquete fue generado por un sistema operativo Windows (que suele usar 128 como valor inicial) y que probablemente aún no ha pasado por muchos saltos.

***¿Por qué es importante el TTL en la red?***<br>
Su importancia es vital para la estabilidad global de Internet:

*Prevención de bucles infinitos:* Si hay un error de configuración en las tablas de enrutamiento y un paquete entra en un bucle (girando entre los mismos routers), el TTL llegará eventualmente a 0.

*Descarte de paquetes:* Cuando el TTL llega a 0, el router descarta el paquete y envía un mensaje ICMP de "Time Exceeded" al origen. Sin el TTL, los paquetes "huérfanos" saturarían los enlaces de red para siempre.

<img width="966" height="82" alt="image" src="https://github.com/user-attachments/assets/c14c39e7-8d5b-453d-b34a-b610a233970a" />

***1. Función de los Flags ACK y PSH***<br>
**ACK (Acknowledgment):** Indica que el número de reconocimiento (Acknowledgment Number) en la cabecera es válido. Se utiliza para confirmar al emisor que los datos enviados anteriormente han sido recibidos correctamente. Es el mecanismo de "acuse de recibo" de TCP.

**PSH (Push):** Le indica al receptor que debe pasar los datos a la aplicación (en este caso, el navegador web) de manera inmediata, sin esperar a que el búfer de recepción se llene. Esto asegura que la interacción sea fluida.

***2. ¿Qué indica el "Puerto Destino: 80"?***<br>
El puerto 80 es el puerto estándar y bien conocido para el protocolo HTTP (HyperText Transfer Protocol).

**Servicio:** Indica que el cliente está intentando acceder a un servidor web para solicitar una página o recurso sin cifrar.

**Contexto de la captura:** Esto coincide perfectamente con los datos del segmento que ves al final de la imagen: "GET /index.html HTTP/1.1", que es una petición web típica.

<img width="961" height="88" alt="image" src="https://github.com/user-attachments/assets/21b3ec78-2521-4103-9b73-00dc71051203" />

Si el paquete de la captura se enviara utilizando el protocolo IPv6 en lugar de IPv4, se producirían cambios estructurales profundos en la comunicación.

***1. La Cabecera de Reemplazo***<br>
La cabecera IPv4 (que en tu captura incluye campos como Protocolo: 6 y TTL: 128) sería reemplazada por la Cabecera Fija de IPv6.<br>

En esta nueva estructura, los campos que viste en la captura cambiarían de nombre y función:
- El campo TTL (Time To Live) de IPv4 se convierte en el campo Hop Limit (Límite de Saltos) en IPv6.<br>
- El campo Protocolo de IPv4 se convierte en el campo Next Header (Siguiente Cabecera) en IPv6.

***2. Mejora notable en el procesamiento por parte de los routers***<br>
La mejora más significativa es la eficiencia en el enrutamiento debido a la simplificación de la cabecera.

**Eliminación del Checksum de Cabecera:** A diferencia de IPv4, la cabecera de IPv6 no tiene un campo de Checksum (suma de verificación).

***¿Por qué es una mejora?*** En IPv4, cada router por el que pasa el paquete debe recalcular el Checksum porque el valor del TTL cambia en cada salto. Esto consume ciclos de CPU en el router. En IPv6, se confía en que las capas superiores (como TCP) o la capa de enlace (Ethernet) manejen la detección de errores, permitiendo que los routers procesen y reenvíen los paquetes mucho más rápido.

**Cabeceras de longitud fija:** La cabecera de IPv6 tiene siempre un tamaño fijo de 40 bytes, lo que facilita su procesamiento por hardware especializado en comparación con la cabecera variable de IPv4.

<img width="1044" height="319" alt="image" src="https://github.com/user-attachments/assets/f8bec04d-2eef-43b0-bd97-2890b9a317b9" /><vbr>
El comando pathping 8.8.8.8 es una herramienta de trazado de ruta que proporciona información mucho más detallada que un simple ping o tracert.

🔴 ***1. ¿Qué información proporciona que no daría un "ping" o un "tracert"?***<br>
Mientras que ping solo te dice si hay conectividad básica y tracert te muestra la ruta (los saltos), pathping ofrece un análisis estadístico de la pérdida de paquetes por cada salto.

**Diferencia con ping:** El ping solo analiza el destino final. pathping analiza cada router intermedio.<br>
**Diferencia con tracert:** El tracert te da la ruta rápida, pero no te dice si un router específico está saturado. pathping identifica exactamente en qué nodo del camino se están perdiendo datos o dónde aumenta la latencia de forma crítica.

🔴 ***2. Proceso que sigue pathping para obtener resultados***<br>
Este comando funciona en dos fases bien diferenciadas:

➖ **Fase 1: Descubrimiento de la Ruta (Tipo Tracert)**<br>
Primero, el comando envía paquetes ICMP con el TTL incrementado para identificar todos los routers (saltos) entre tu equipo y el destino (en este caso, los servidores DNS de Google, 8.8.8.8). Esta parte es rápida.

➖ **Fase 2: Análisis de Estadísticas (El "Periodo de Cómputo")**<br>
Una vez identificada la ruta, pathping se queda "escuchando" durante un tiempo determinado (normalmente 250 segundos).
- Envía múltiples paquetes a cada uno de los routers identificados en la Fase 1.<br>
- Calcula el porcentaje de paquetes devueltos y perdidos por cada salto.<br>
- Al finalizar, muestra una tabla detallada con los resultados de latencia y pérdida de paquetes para cada router.

<img width="946" height="305" alt="image" src="https://github.com/user-attachments/assets/6d302c78-f200-469f-82c2-278884480984" /><br>
Basándonos en el escenario de un router con SNMPv2c y comunidad "public", estas son las soluciones:

🔵 ***1. Herramienta para "caminar" por el árbol MIB***<br>
Para obtener todos los valores de la interfaz del router en la IP 192.168.1.1, la herramienta estándar de línea de comandos es snmpwalk.

- **Cómo funciona:** Este comando realiza peticiones GetNext de forma sucesiva y automática. Empieza en un punto del árbol MIB y va "saltando" de OID en OID hasta recorrer toda la rama especificada, permitiéndote ver toda la configuración y estado del dispositivo de una sola vez.

- **Ejemplo de uso:** snmpwalk -v 2c -c public 192.168.1.1

🔵 ***2. Análisis del mensaje "authenticationFailure" Trap***<br>
Evento que lo provoca: Este Trap específico se dispara cuando alguien intenta acceder al router mediante SNMP utilizando una cadena de comunidad incorrecta (por ejemplo, escribir "admin" en lugar de "public"). Es una alerta de seguridad que indica un posible acceso no autorizado o un error de configuración en un gestor.

🟢 ***Ventaja del Trap frente al Polling (consulta constante):***<br>
- **Inmediatez: El Trap es enviado por el router en el mismo instante en que ocurre el error. Si usaras polling, tendrías que esperar hasta el siguiente ciclo de consulta (que podría ser minutos después) para enterarte.<br>
- **Eficiencia de red:** El polling consume ancho de banda y CPU constantemente al preguntar "¿estás bien?" repetidamente. El Trap es pasivo; no genera tráfico hasta que realmente sucede algo importante, ahorrando recursos valiosos en la red.
