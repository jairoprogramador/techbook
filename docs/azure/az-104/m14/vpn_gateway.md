# VPN Gateway (Azure)

VPN Gateway en Azure es como la puerta de enlace que une tu red virtual con el exterior: ya sea con usuarios que se conectan desde su casa (punto a sitio), con tu oficina local (sitio a sitio) o con otra red virtual de Azure (VNet a VNet). No es la conexión en sí; es el recurso que se despliega en una subred especial (GatewaySubnet) y que permite crear y mantener esos túneles cifrados. Según la SKU que elijas, tendrás más o menos rendimiento y disponibilidad; puede funcionar en modo activo-en espera o activo-activo para mayor disponibilidad.

## Definición

VPN Gateway es un tipo de Virtual Network Gateway en Azure que permite tráfico cifrado entre una red virtual y ubicaciones externas (clientes, redes locales u otras redes virtuales) mediante conexiones punto a sitio (P2S), sitio a sitio (S2S) o VNet a VNet; se despliega en una subred dedicada llamada GatewaySubnet y tiene SKUs que determinan rendimiento y características.

Permite:

- Conectar clientes individuales a la VNet (VPN punto a sitio).
- Conectar una red local a la VNet mediante túnel IPsec/IKE (VPN sitio a sitio).
- Conectar dos redes virtuales entre sí mediante túnel (VPN VNet a VNet).
- Usar modos activo-en espera o activo-activo para disponibilidad.
- Opcionalmente habilitar BGP para enrutamiento dinámico y forced tunneling para enviar todo el tráfico de Internet por el túnel hacia local.

## Componentes

**Virtual Network Gateway (tipo VPN)** – Recurso de Azure que representa la puerta de enlace VPN; se crea en una VNet y se despliega en la GatewaySubnet.

**GatewaySubnet** – Subred dedicada que debe tener el nombre "GatewaySubnet"; contiene las instancias del gateway; no se pueden desplegar otras cargas de trabajo en ella; el tamaño mínimo recomendado depende de la configuración (p. ej. /27 o mayor para algunas SKUs).

**SKU del gateway** – Nivel de rendimiento y características: VpnGw1 a VpnGw5 (y variantes con redundancia de zona VpnGw1AZ a VpnGw5AZ); la SKU determina throughput, número de túneles y si admite redundancia de zona.

**Dirección IP pública** – El gateway obtiene una o dos direcciones IP públicas (una en activo-en espera, dos en activo-activo) que son el punto de terminación del túnel VPN.

**Modo activo-en espera** – Una instancia activa del gateway; la otra en espera; conmutación automática en caso de fallo.

**Modo activo-activo** – Dos instancias activas con dos IP públicas; mayor disponibilidad y throughput; requiere segunda IP pública.

**BGP** – Protocolo de enrutamiento dinámico opcional; permite intercambiar rutas entre el gateway y dispositivos locales sin configurar rutas estáticas manualmente.

**Forced tunneling** – Opción para enrutar todo el tráfico con destino a Internet desde las VMs de la VNet a través del túnel S2S hacia la red local para inspección o auditoría.

## Funcionalidad

1. Se crea una subred llamada "GatewaySubnet" en la VNet (tamaño suficiente, p. ej. /27)
2. Se crea el recurso Virtual Network Gateway de tipo VPN en la misma VNet y región; se asocia a la GatewaySubnet
3. Se elige la SKU (VpnGw1 a VpnGw5 o variantes AZ) según rendimiento y requisitos de zona
4. El gateway obtiene una o dos direcciones IP públicas según el modo (activo-en espera o activo-activo)
5. Se crean las conexiones: configuración P2S (clientes), S2S (red local) o VNet-to-VNet (otra VNet)
6. Opcionalmente se habilita BGP en la conexión para enrutamiento dinámico
7. Para S2S se puede configurar forced tunneling para que el tráfico a Internet salga por el túnel hacia local
8. El despliegue del gateway puede tardar 45 minutos o más según la SKU

## Casos de Uso

- Dar acceso remoto a usuarios (desarrolladores, soporte) a recursos de la VNet mediante VPN punto a sitio
- Conectar la sede central o sucursales (red local) a Azure mediante VPN sitio a sitio
- Conectar dos VNets de Azure (distintas regiones o suscripciones) mediante VPN VNet a VNet
- Aumentar disponibilidad y throughput con modo activo-activo y BGP
- Cumplir requisitos de seguridad enviando todo el tráfico a Internet por la red local (forced tunneling)
- Usar gateways con redundancia de zona (SKU AZ) para resiliencia en la región

## Errores Comunes

- Confundir VPN Gateway con VNet peering (el gateway usa túneles VPN cifrados; el peering es conexión nativa de Azure sin gateway VPN)
- Desplegar otras máquinas o servicios en la GatewaySubnet (solo el gateway debe estar en esa subred)
- Usar un tamaño de GatewaySubnet insuficiente (debe ser al menos /27 y según SKU; /26 para algunas configuraciones)
- Pensar que se puede cambiar la SKU del gateway sin tiempo de inactividad (el cambio puede implicar recrear o actualizar con downtime)
- Creer que forced tunneling aplica a P2S (forced tunneling es para conexiones S2S; el tráfico de clientes P2S se enruta según la configuración del cliente)

## Preguntas

1. ¿VPN Gateway es un tipo de Virtual Network Gateway que permite conexiones P2S, S2S y VNet-to-VNet?

2. ¿El gateway VPN se despliega en una subred dedicada llamada "GatewaySubnet" y no se pueden desplegar otras cargas de trabajo en ella?

3. ¿La SKU del gateway (VpnGw1 a VpnGw5) determina el rendimiento, número de túneles y si admite redundancia de zona?

4. ¿En modo activo-activo el gateway tiene dos direcciones IP públicas y dos instancias activas para mayor disponibilidad?

5. ¿Forced tunneling enruta todo el tráfico con destino a Internet desde la VNet a través del túnel S2S hacia la red local?

6. ¿BGP en el gateway permite enrutamiento dinámico entre Azure y los dispositivos VPN locales?
