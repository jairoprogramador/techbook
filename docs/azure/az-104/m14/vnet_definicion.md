# Red virtual (VNet)

Una red virtual (VNet) en Azure es como un barrio privado dentro de la nube: defines el rango de direcciones del barrio (address space), lo divides en manzanas (subredes) y las máquinas que viven ahí se pueden hablar entre sí sin salir a la calle pública. La VNet pertenece a una región; las subredes y los recursos que creas dentro (VMs, gateways, etc.) usan ese espacio de direcciones. Por defecto Azure ya pone las rutas necesarias para que el tráfico fluya entre subredes y hacia Internet; si quieres cambiar el comportamiento (p. ej. enviar tráfico por un firewall), usas rutas definidas por el usuario (UDR).

## Definición

Una red virtual (VNet) es un recurso de Azure que representa una red privada aislada dentro de la infraestructura de Azure; tiene un espacio de direcciones (CIDR), pertenece a una región y se divide en subredes; los recursos desplegados en las subredes pueden comunicarse entre sí y con Internet según las rutas y los NSG configurados.

Permite:

- Segmentar la red mediante subredes (rangos de IP dentro del address space)
- Enrutamiento interno automático entre subredes de la misma VNet
- Integración con servicios PaaS (Service Endpoint, Private Endpoint), VPN Gateway y ExpressRoute
- Asociar un NSG a subredes o interfaces de red para filtrar tráfico
- Sobrescribir el enrutamiento por defecto mediante tablas de rutas (UDR) asociadas a subredes
- Resolución DNS interna (Azure-provided DNS) y opcionalmente DNS propio o privado (Azure DNS Private Zones)

## Componentes

**Address space (espacio de direcciones)** – Rango de direcciones privadas en notación CIDR (p. ej. 10.0.0.0/16) que define el “barrio”; las subredes son rangos dentro de este espacio que no se solapan

**Subred** – Segmento del address space asignado a una subred (p. ej. 10.0.1.0/24); cada recurso (VM, gateway, etc.) se despliega en una subred; Azure reserva algunas direcciones en cada subred

**Región** – La VNet existe en una sola región; las subredes y los recursos de la VNet están en esa región (salvo servicios que permitan multi-región)

**Rutas del sistema** – Rutas que Azure crea por defecto (tráfico entre subredes, a Internet, a la red virtual, etc.); no se pueden eliminar pero se pueden sobrescribir con UDR

**DNS** – Por defecto Azure proporciona resolución DNS (nombre de la VM resuelve a IP privada); se puede configurar servidor DNS propio o Azure DNS Private Zones

**Peering** – Conexión entre dos VNets (misma región o global) que permite tráfico entre ellas sin gateway VPN; los espacios de direcciones no deben solaparse

## Funcionalidad

1. Se crea una VNet en una suscripción y en una región; se define el address space (p. ej. 10.0.0.0/16)
2. Se crean subredes dentro del address space (p. ej. 10.0.1.0/24 para VMs, 10.0.2.0/24 para gateway); los rangos no se solapan
3. Los recursos (VMs, VPN Gateway, etc.) se despliegan en una subred; reciben una IP privada del rango de la subred
4. El tráfico entre subredes de la misma VNet se enruta automáticamente por las rutas del sistema
5. Se pueden asociar NSG a subredes o a interfaces de red para permitir o denegar tráfico
6. Se pueden asociar tablas de rutas (UDR) a subredes para sobrescribir del próximo salto (p. ej. enviar tráfico a un appliance de seguridad)
7. Se puede conectar la VNet a otras VNets (peering), a redes on-premise (VPN Gateway, ExpressRoute) o a servicios PaaS (Service Endpoint, Private Endpoint)

## Casos de Uso

- Crear una red privada para VMs y servicios en una región
- Segmentar por subredes (front-end, back-end, datos, gateway) para seguridad y organización
- Conectar la VNet a la red local mediante VPN Gateway o ExpressRoute
- Conectar dos VNets mediante peering (sin gateway VPN)
- Forzar tráfico por un firewall (NVA) usando UDR
- Integrar con Azure DNS Private Zones para resolución DNS privada

## Errores Comunes

- Definir subredes con rangos que se solapan dentro del mismo address space (cada subred debe ser un bloque único)
- Creer que una VNet puede abarcar varias regiones (una VNet está en una sola región; para otras regiones se crea otra VNet y opcionalmente peering global)
- Confundir VNet con suscripción (la VNet es un recurso dentro de una suscripción; puede haber varias VNets por suscripción)
- Pensar que el tráfico entre subredes no se puede filtrar (los NSG permiten filtrar; las rutas del sistema permiten el tráfico por defecto)
- Solapar address spaces entre VNets que se van a emparejar (peering requiere espacios no solapados)

## Preguntas

1. ¿Una red virtual (VNet) es un recurso de Azure que representa una red privada con un espacio de direcciones y subredes en una región?.

2. ¿Las subredes son segmentos del address space de la VNet y los rangos no deben solaparse?.

3. ¿Una VNet existe en una sola región?.

4. ¿Azure crea rutas del sistema por defecto para tráfico entre subredes y a Internet que se pueden override con UDR?.

5. ¿Para conectar dos VNets sin gateway VPN se usa peering y los espacios de direcciones no deben solaparse?.

6. ¿Los recursos (VMs, gateway) se despliegan en una subred y reciben una IP privada del rango de esa subred?.
