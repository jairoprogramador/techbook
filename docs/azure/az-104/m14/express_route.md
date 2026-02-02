# ExpressRoute

ExpressRoute es como tener una línea privada dedicada entre tu oficina y el datacenter de Microsoft: el tráfico no va por Internet, sino por un circuito privado que un proveedor de conectividad (operador o Exchange) te proporciona. No hay cifrado VPN ni IP público expuesto en Internet para ese enlace; es una conexión privada, con mayor rendimiento y menor latencia que una VPN sitio a sitio. Sirve para conectar tu red local a redes virtuales de Azure y a servicios de Microsoft (Microsoft 365, Dynamics) de forma privada.

## Definición

ExpressRoute es un servicio de Azure que permite conectar la red local a redes virtuales de Azure y a servicios en la nube de Microsoft (Microsoft 365, Dynamics, etc.) mediante un circuito privado que no atraviesa Internet; el circuito se contrata con un proveedor de conectividad (Exchange, operador o conexión Any-to-Any) y se configura con peerings (Private peering para VNets, Microsoft peering para servicios Microsoft).

Permite:

- Conectar la red local a Azure de forma privada (sin tráfico por Internet público)
- Mayor throughput, menor latencia y mayor disponibilidad que VPN sitio a sitio para tráfico híbrido
- Private peering: conectividad desde la red local a las redes virtuales de Azure
- Microsoft peering: conectividad a servicios Microsoft (Microsoft 365, Dynamics, Azure PaaS por Microsoft peering)
- No reemplaza la necesidad de un VPN Gateway en la VNet: el circuito ExpressRoute se enlaza a un Virtual Network Gateway de tipo ExpressRoute en la VNet

## Componentes

**Circuito ExpressRoute** – Recurso lógico que representa la conexión entre tu red y Microsoft; se crea en Azure y se provisiona con un proveedor de conectividad; tiene un identificador (service key) y un ancho de banda contratado

**Proveedor de conectividad** – Operador o Exchange que proporciona el circuito físico hasta los routers de Microsoft (peering location); tú o el proveedor configuran el circuito y el BGP con Microsoft

**Peering location** – Ubicación donde los routers de Microsoft se conectan con el proveedor; una vez conectado al peering location, puedes acceder a servicios de Azure en todas las regiones (según nivel del circuito)

**Private peering** – Peering BGP entre tu red y las redes virtuales de Azure; permite conectividad desde local a las VNets; se configura en el circuito ExpressRoute y se enlaza a un Virtual Network Gateway (tipo ExpressRoute) en la VNet

**Microsoft peering** – Peering BGP entre tu red y Microsoft para acceder a servicios Microsoft (Microsoft 365, Dynamics, Azure PaaS con endpoints públicos por Microsoft peering); opcional y distinto de Private peering

**Virtual Network Gateway (tipo ExpressRoute)** – Gateway en la VNet de tipo ExpressRoute (no VPN); el circuito ExpressRoute se “conecta” a este gateway para que el tráfico entre la red local y la VNet fluya por el circuito privado

**BGP** – Protocolo de enrutamiento usado entre tu red y Microsoft para intercambiar rutas; cada peering (Private, Microsoft) usa sesiones BGP

## Funcionalidad

1. Se contrata un circuito ExpressRoute con un proveedor de conectividad en un peering location
2. Se crea el recurso “ExpressRoute circuit” en Azure; el proveedor provisiona el circuito y lo habilita
3. Se configura el peering en el circuito: Private peering (para VNets) y opcionalmente Microsoft peering (para servicios Microsoft)
4. Se crea un Virtual Network Gateway de tipo ExpressRoute en la VNet (subred GatewaySubnet)
5. Se crea una conexión entre el circuito ExpressRoute y el gateway (enlazar el circuito al gateway)
6. En la red local se configura BGP con Microsoft (direcciones y ASN según documentación); las rutas se intercambian por BGP
7. El tráfico entre la red local y la VNet fluye por el circuito privado sin pasar por Internet
8. El tráfico a servicios Microsoft (si se usa Microsoft peering) también fluya por el circuito según la configuración de rutas

## Casos de Uso

- Conectar la sede central o datacenter a Azure con mayor rendimiento y menor latencia que VPN S2S
- Cumplir requisitos de compliance o seguridad que exigen que el tráfico no pase por Internet
- Conectar a Microsoft 365 o Dynamics por Microsoft peering de forma privada
- Combinar ExpressRoute con VPN S2S como enlace de respaldo (coexistencia)
- Contratar niveles de ancho de banda y SLA superiores a los de VPN

## Errores Comunes

- Confundir ExpressRoute con VPN Gateway (ExpressRoute es un circuito privado sin Internet; VPN Gateway usa túneles por Internet)
- Pensar que el circuito ExpressRoute no necesita un gateway en la VNet (se necesita un Virtual Network Gateway de tipo ExpressRoute en la VNet y enlazar el circuito a ese gateway)
- Creer que con solo crear el circuito en Azure ya hay conectividad (el proveedor debe provisionar el circuito y tú o el proveedor deben configurar BGP)
- Confundir Private peering con Microsoft peering (Private = conectividad a VNets de Azure; Microsoft = conectividad a servicios Microsoft como Microsoft 365)
- Asumir que ExpressRoute cifra el tráfico por defecto (el circuito es privado pero no es un túnel IPsec; si se requiere cifrado, se puede usar IPsec sobre el circuito)

## Preguntas

1. ¿ExpressRoute conecta la red local a Azure mediante un circuito privado que no atraviesa Internet?

2. ¿El circuito ExpressRoute se contrata con un proveedor de conectividad y se configura con peerings (Private, Microsoft)?

3. ¿Private peering en ExpressRoute permite conectividad desde la red local a las redes virtuales de Azure?

4. ¿Para que el tráfico entre la red local y una VNet use ExpressRoute hay que crear un Virtual Network Gateway de tipo ExpressRoute en la VNet y enlazar el circuito a ese gateway?

5. ¿Microsoft peering en ExpressRoute permite conectividad a servicios Microsoft (Microsoft 365, etc.) de forma privada?

6. ¿ExpressRoute usa BGP para intercambiar rutas entre la red local y Microsoft?
