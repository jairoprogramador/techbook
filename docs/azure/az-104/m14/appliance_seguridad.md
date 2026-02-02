# Appliance de seguridad (NVA)

Un appliance de seguridad (NVA) en Azure es como poner un guardia en la puerta de tu red: una VM o un dispositivo virtual que inspecciona y filtra el tráfico (firewall, IDS/IPS, proxy). No es un servicio gestionado de Azure; es una VM (o conjunto de VMs) que tú despliegas y configuras. Para que todo el tráfico pase por ese “guardia”, usas rutas definidas por el usuario (UDR): en la tabla de rutas indicas que el tráfico con cierto destino (p. ej. 0.0.0.0/0) tiene como próximo salto la IP del NVA. Así el tráfico se fuerza por el appliance en lugar de ir directo a Internet o entre subredes.

## Definición

Un appliance de seguridad o NVA (Network Virtual Appliance) en Azure es una VM (o conjunto de VMs) que actúa como firewall, proxy, IDS/IPS o similar para inspeccionar y filtrar el tráfico de red; no es un servicio nativo de Azure (como Azure Firewall); se despliega en una subred de la VNet y el tráfico se dirige hacia él mediante rutas definidas por el usuario (UDR) que usan el próximo salto “Virtual Appliance”.

Permite:

- Inspeccionar y filtrar tráfico (entrante o saliente) según reglas de firewall o políticas propias del NVA.
- Forzar tráfico por el NVA usando UDR (p. ej. 0.0.0.0/0 con próximo salto = IP del NVA).
- Implementar topologías hub-and-spoke donde el hub contiene el NVA y los spokes enrutan su tráfico hacia el hub.
- Usar ofertas de terceros (Barracuda, Palo Alto, etc.) o una VM con software de firewall; la VM debe tener IP forwarding habilitado para reenviar paquetes.

## Componentes

**NVA (Network Virtual Appliance)** – VM (o conjunto de VMs) que ejecuta software de firewall, proxy, IDS/IPS u otro dispositivo de seguridad; se despliega en una subred de la VNet.

**Subred del NVA** – Subred dedicada donde se despliega el NVA (p. ej. subred “DMZ” o “Firewall”); la IP del NVA es la que se usa como próximo salto en las UDR.

**UDR (tabla de rutas)** – Tabla de rutas asociada a subredes (p. ej. spokes) con rutas que apuntan al NVA (próximo salto Virtual Appliance = IP del NVA) para que el tráfico pase por el NVA.

**IP forwarding** – Propiedad de la NIC de la VM que debe estar habilitada para que la VM reenvíe paquetes que no van destinados a ella (necesaria para que el NVA actúe como router/firewall).

**Topología hub-and-spoke** – Diseño donde una VNet “hub” contiene el NVA (y a menudo el gateway VPN/ExpressRoute) y las VNets o subredes “spoke” enrutan su tráfico hacia el hub mediante peering y UDR.

**Azure Firewall** – Servicio gestionado de Azure que también actúa como firewall; alternativa al NVA cuando se prefiere un servicio nativo en lugar de una VM de terceros.

## Funcionalidad

1. Se despliega una VM con software de firewall o un NVA de terceros en una subred de la VNet (p. ej. subred dedicada).
2. Se habilita IP forwarding en la NIC de la VM para que pueda reenviar tráfico.
3. Se crea una tabla de rutas con rutas que envían el tráfico deseado al NVA: próximo salto Virtual. Appliance = IP privada del NVA (p. ej. ruta 0.0.0.0/0 para todo el tráfico a Internet).
4. Se asocia la tabla de rutas a las subredes que deben enviar su tráfico por el NVA (p. ej. subredes de aplicaciones en un spoke).
5. El tráfico que sale de esas subredes y coincide con el prefijo de la ruta (p. ej. 0.0.0.0/0) se envía al NVA; el NVA inspecciona, filtra y reenvía o descarta según sus reglas.
6. Los NSG deben permitir el tráfico entre las subredes de origen y el NVA, y entre el NVA y el destino (o Internet).
7. En topología hub-and-spoke, el hub tiene el NVA; los spokes tienen UDR que apuntan al NVA del hub (vía peering y direccionamiento correcto).

## Casos de Uso

- Inspeccionar y filtrar todo el tráfico a Internet desde subredes de aplicaciones usando un firewall (NVA) y UDR 0.0.0.0/0 .
- Topología hub-and-spoke: hub con NVA y gateway; spokes con UDR que envían tráfico al hub.
- Cumplir requisitos de seguridad o compliance usando un firewall de terceros (Palo Alto, Barracuda, etc.) en lugar de solo NSG.
- Actuar como proxy o IDS/IPS para tráfico entre subredes o hacia Internet.
- Comparar NVA (VM propia) con Azure Firewall (servicio gestionado) según costo, características y operación.

## Errores Comunes

- Desplegar el NVA pero no configurar UDR (el tráfico no pasará por el NVA; seguirá las rutas del sistema por defecto).
- No habilitar IP forwarding en la NIC del NVA (la VM no reenviará paquetes y el tráfico se perderá o no llegará al destino).
- Bloquear con NSG el tráfico entre las subredes de origen y el NVA o entre el NVA y el destino (hay que permitir los flujos necesarios).
- Poner la IP del NVA en una ruta UDR sin que esa IP sea alcanzable desde la subred (misma VNet, peering o conexión correcta).
- Confundir NVA con Azure Firewall (NVA es una VM que tú gestionas; Azure Firewall es un servicio PaaS de Azure).

## Preguntas

1. ¿Un appliance de seguridad (NVA) en Azure es una VM que actúa como firewall o dispositivo de seguridad y el tráfico se dirige a ella mediante UDR?.

2. ¿Para que el tráfico pase por el NVA hay que crear rutas (UDR) con próximo salto “Virtual Appliance” igual a la IP del NVA?.

3. ¿La VM que actúa como NVA debe tener IP forwarding habilitado en la NIC para reenviar tráfico?.

4. ¿El NVA es una VM que tú despliegas y gestionas, a diferencia de Azure Firewall que es un servicio gestionado de Azure?.

5. ¿En topología hub-and-spoke el tráfico de los spokes se puede forzar hacia un NVA en el hub mediante UDR (y peering)?.

6. ¿Los NSG deben permitir el tráfico entre las subredes de origen y el NVA y entre el NVA y el destino para que el flujo funcione?.
