# VPN Sitio a Sitio (Site-to-Site, S2S)

VPN sitio a sitio es como tender un túnel cifrado entre tu oficina y el datacenter de Azure: toda la red de la oficina (o sucursal) puede hablar con los recursos de la red virtual de Azure como si estuvieran en la misma red. En tu sede necesitas un dispositivo VPN (router o firewall) con IP pública que establezca el túnel con el VPN Gateway de Azure. El tráfico entre ambas redes va cifrado por Internet. Puedes conectar varias sedes a la misma VNet (multi-site) y usar BGP o forced tunneling para enrutar todo el tráfico de Internet por tu red local.

## Definición

VPN sitio a sitio (S2S) es una conexión VPN entre una red local (on-premises) y una red virtual de Azure mediante un túnel IPsec/IKE a través de Internet; requiere un dispositivo VPN en la red local con IP pública y una puerta de enlace VPN (VPN Gateway) en la VNet; el tráfico entre ambas redes va cifrado.

Permite:

- Conectar la red de la sede central o sucursales a una VNet de Azure (configuración híbrida)
- Conectar varias redes locales a la misma VNet (multi-site) con varias conexiones S2S
- Usar BGP para enrutamiento dinámico entre el gateway y el dispositivo local
- Configurar forced tunneling para que todo el tráfico con destino a Internet desde la VNet salga por el túnel hacia la red local para inspección o cumplimiento
- Usar modo activo-activo en el gateway para mayor disponibilidad y throughput

## Componentes

**Local network gateway** – Recurso en Azure que representa tu red local: nombre, IP pública del dispositivo VPN local y espacios de direcciones (CIDR) de la red local

**VPN Gateway** – Puerta de enlace VPN en la VNet que termina el túnel S2S; debe tener una conexión de tipo "Site-to-site (IPsec)"

**Conexión S2S** – Recurso que vincula el VPN Gateway con el Local network gateway; define la clave precompartida (PSK), protocolo (IKEv1/IKEv2) y opciones (BGP, etc.)

**Dispositivo VPN local** – Router, firewall o appliance en la red local con IP pública que establece el túnel IPsec con el VPN Gateway; debe ser compatible con Azure (lista de dispositivos probados en documentación Microsoft)

**Clave precompartida (PSK)** – Secreto compartido entre el gateway y el dispositivo VPN local para autenticación del túnel; debe coincidir en ambos lados

**BGP** – Opcional; permite intercambiar rutas dinámicamente entre el VPN Gateway y el dispositivo local; evita configurar rutas estáticas para cada prefijo

**Forced tunneling** – Configuración que obliga a que todo el tráfico con destino a Internet desde las VMs de la VNet pase por el túnel S2S hacia la red local (default route 0.0.0.0/0 hacia el túnel)

**Multi-site** – Varias conexiones S2S desde el mismo VPN Gateway a distintos Local network gateways (varias sedes a la misma VNet)

## Funcionalidad

1. Se crea el VPN Gateway en la VNet (GatewaySubnet) con tipo VPN y SKU que soporte S2S
2. Se crea un recurso "Local network gateway" con la IP pública del dispositivo VPN local y los espacios de direcciones de la red local
3. Se crea una conexión de tipo "Site-to-site (IPsec)" entre el VPN Gateway y el Local network gateway; se configura la clave precompartida (y opcionalmente BGP)
4. En el dispositivo VPN local se configura el túnel hacia la IP pública del VPN Gateway, la PSK y los espacios de direcciones de la VNet
5. Una vez establecido el túnel, el tráfico entre la red local y la VNet viaja cifrado por IPsec
6. Opcionalmente se habilita BGP en la conexión para que las rutas se intercambien dinámicamente
7. Opcionalmente se configura forced tunneling en el gateway para enviar el tráfico a Internet por el túnel hacia local
8. Para multi-site se crean varios Local network gateways y varias conexiones S2S al mismo VPN Gateway (dentro de los límites de la SKU)

## Casos de Uso

- Conectar la sede central a Azure para acceso híbrido (VMs, aplicaciones en la VNet accesibles desde la red local)
- Conectar varias sucursales a la misma VNet (multi-site) con una VPN Gateway
- Usar BGP para no mantener rutas estáticas cuando cambian las redes locales
- Cumplir políticas de seguridad enviando todo el tráfico a Internet por la red local (forced tunneling) para inspección o auditoría
- Aumentar disponibilidad con modo activo-activo y BGP en el gateway

## Errores Comunes

- Confundir S2S con P2S: S2S es red local a VNet (dispositivo VPN en sede); P2S es un cliente individual a VNet
- Pensar que el dispositivo VPN local no necesita IP pública (debe tener IP pública para que el VPN Gateway de Azure establezca el túnel)
- Configurar una PSK distinta en Azure y en el dispositivo local (deben coincidir o el túnel no se establecerá)
- Definir en Local network gateway espacios de direcciones que se solapan con la VNet (deben ser los prefijos reales de la red local, sin solapar con la VNet)
- Creer que forced tunneling se aplica a clientes P2S (forced tunneling es solo para tráfico que sale de la VNet en conexiones S2S; el tráfico de clientes P2S no pasa por la misma ruta por defecto)

## Preguntas

1. ¿VPN sitio a sitio (S2S) conecta una red local a una VNet de Azure mediante un túnel IPsec a través de Internet?

2. ¿S2S requiere un dispositivo VPN en la red local con IP pública y un VPN Gateway en la VNet?

3. ¿El recurso "Local network gateway" en Azure representa la red local: IP pública del dispositivo VPN y espacios de direcciones de la red local?

4. ¿La clave precompartida (PSK) debe ser la misma en la conexión S2S en Azure y en el dispositivo VPN local para que el túnel se establezca?

5. ¿Forced tunneling hace que todo el tráfico con destino a Internet desde la VNet salga por el túnel S2S hacia la red local?

6. ¿Se pueden conectar varias redes locales (multi-site) a la misma VNet creando varios Local network gateways y varias conexiones S2S al mismo VPN Gateway?
