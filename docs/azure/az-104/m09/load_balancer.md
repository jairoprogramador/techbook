# Azure Load Balancer

Azure Load Balancer es como el repartidor que distribuye las peticiones entre varios servidores sin mirar el contenido del paquete: solo mira el puerto y el protocolo (TCP o UDP) y envía el tráfico a uno de los servidores del grupo que esté sano. No entiende HTTP ni URLs; reparte conexiones de red de forma rápida y con poco retraso. Puede ser público (entrada desde Internet) o interno (solo dentro de la red virtual). Sirve para equilibrar carga de bases de datos, APIs TCP/UDP o cualquier tráfico que no requiera decisiones basadas en la URL o en el contenido HTTP.

## Definición

Azure Load Balancer es un equilibrador de carga de capa 4 (transporte) que distribuye tráfico TCP, UDP o ICMP entre instancias de un grupo de backends (VMs, VM Scale Sets); puede ser público (con IP pública, tráfico desde Internet) o interno (solo dentro de la VNet); ofrece alto rendimiento y baja latencia y no inspecciona el contenido de la aplicación (HTTP, URL, etc.).

Permite:

- Distribuir tráfico entrante entre varias VMs o instancias de un VM Scale Set (grupo de backends)
- Operar en capa 4 (TCP, UDP): no inspecciona HTTP ni URLs; solo puerto y protocolo
- Configurar un Load Balancer público (con IP pública) o interno (solo tráfico dentro de la VNet)
- Usar health probes (TCP o HTTP) para comprobar que los backends están sanos y dejar de enviar tráfico a los que fallen
- Definir reglas de equilibrio de carga (puerto frontend → puerto backend) y reglas NAT de entrada (puerto frontend → una VM concreta); en cada regla se puede configurar el modo de distribución (Session persistence); ver **Load Balancer Affinity**
- Integrar con VM Scale Sets para distribuir tráfico entre las instancias del scale set
- Ofrecer alto throughput y baja latencia al no procesar contenido de capa 7

## Componentes

**Frontend** – Configuración del lado que recibe el tráfico: una o más direcciones IP (pública o privada según el tipo de Load Balancer) y puerto

**Backend pool** – Conjunto de destinos (NICs de VMs o configuración del VM Scale Set) entre los que se distribuye el tráfico; todas las instancias del pool reciben tráfico según la regla de equilibrio

**Regla de equilibrio de carga (load balancing rule)** – Asocia un frontend (IP:puerto) con un backend pool y un puerto; define el protocolo (TCP o UDP) y el modo de distribución (Session persistence); el tráfico que llega al frontend se distribuye entre los backends del pool (detalle de affinity en **Load Balancer Affinity**)

**Regla NAT de entrada (inbound NAT rule)** – Asocia un puerto del frontend con una VM concreta del backend (no equilibrio; tráfico directo a esa VM); útil para RDP, SSH u otro acceso directo a una instancia

**Health probe (sonda de salud)** – Comprueba periódicamente si los backends responden (TCP o HTTP); si un backend no responde, se deja de enviar tráfico hasta que vuelva a estar sano

**Load Balancer público** – Tipo de Load Balancer con IP pública; recibe tráfico desde Internet y lo distribuye a los backends

**Load Balancer interno** – Tipo de Load Balancer sin IP pública; recibe tráfico solo desde dentro de la VNet (por ejemplo, entre capas de una aplicación)

**Capa 4 (transporte)** – Nivel del modelo OSI en el que opera; solo ve IP, puerto y protocolo (TCP/UDP); no inspecciona HTTP, URL ni headers

## Funcionalidad

1. Se crea un recurso Load Balancer (público o interno) en una VNet y región
2. Se configura el frontend: IP pública (público) o IP privada de una subred (interno)
3. Se crea un backend pool y se añaden las VMs (NICs) o se asocia el VM Scale Set
4. Se configura un health probe (TCP o HTTP) para comprobar el estado de los backends
5. Se crea una regla de equilibrio de carga: frontend (IP:puerto) → backend pool (puerto), protocolo TCP o UDP; opcionalmente se configura Session persistence (ver **Load Balancer Affinity**)
6. Opcionalmente se crean reglas NAT de entrada para enviar tráfico de un puerto del frontend a una VM concreta (p. ej. RDP, SSH)
7. El Load Balancer distribuye las nuevas conexiones entre los backends sanos del pool; no envía tráfico a backends que fallen el health probe
8. No realiza terminación SSL ni enrutamiento por URL; opera solo en capa 4

## Casos de Uso

- Equilibrar carga de tráfico TCP o UDP entre varias VMs o instancias de un VM Scale Set
- Exponer una aplicación web o API detrás de un Load Balancer público sin necesidad de enrutamiento por URL ni SSL en el balanceador
- Load Balancer interno para distribuir tráfico entre capas (por ejemplo, front-end → back-end) dentro de la VNet
- Alta disponibilidad y escalado horizontal: añadir más VMs al backend pool o usar VM Scale Sets con Load Balancer
- Acceso directo a una VM concreta (RDP, SSH) mediante reglas NAT de entrada
- Cargas de trabajo que requieren alto throughput y baja latencia sin inspección HTTP

## Errores Comunes

- Confundir Load Balancer con Application Gateway (Load Balancer es capa 4, TCP/UDP; Application Gateway es capa 7, HTTP/HTTPS, con enrutamiento por URL, SSL y WAF)
- Pensar que Load Balancer puede enrutar por URL o path (no puede; para eso se usa Application Gateway)
- Creer que Load Balancer hace terminación SSL (no la hace; el SSL termina en las VMs del backend o se usa Application Gateway)
- Configurar un health probe que no coincida con el puerto o ruta que realmente usa la aplicación (el backend puede marcarse como no sano incorrectamente)
- Usar solo Load Balancer cuando se necesita WAF o enrutamiento por host/path (en esos casos Application Gateway es más adecuado)

## Preguntas

1. ¿Azure Load Balancer opera en capa 4 (TCP, UDP) y distribuye tráfico entre los backends de un pool sin inspeccionar contenido HTTP?

2. ¿Load Balancer puede ser público (con IP pública) o interno (solo tráfico dentro de la VNet)?

3. ¿El health probe comprueba si los backends están sanos y el Load Balancer deja de enviar tráfico a los que fallen?

4. ¿La regla de equilibrio de carga asocia un frontend (IP:puerto) con un backend pool y distribuye las conexiones entre los backends sanos?

5. ¿La regla NAT de entrada envía el tráfico de un puerto del frontend a una VM concreta (sin equilibrio), útil para RDP o SSH?

6. ¿Load Balancer no realiza terminación SSL ni enrutamiento por URL a diferencia de Application Gateway?
