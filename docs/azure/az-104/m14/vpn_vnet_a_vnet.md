# VPN VNet a VNet (VNet-to-VNet)

VPN VNet a VNet es como unir dos edificios de la misma empresa en ciudades distintas con un túnel privado: cada edificio es una red virtual de Azure. El tráfico entre ambas redes va cifrado por la red de Microsoft (no por Internet público) y cada lado tiene su propia puerta de enlace VPN. No es VNet peering: el peering es una conexión nativa de Azure sin cifrado ni gateway; VNet-to-VNet usa túneles IPsec entre dos VPN Gateways. Sirve cuando quieres cifrado explícito o cuando las redes están en distintas suscripciones o regiones y el peering no cubre el caso.

## Definición

VPN VNet a VNet es una conexión entre dos redes virtuales de Azure mediante túneles IPsec/IKE entre dos VPN Gateways (uno en cada VNet); el tráfico entre las VNets va cifrado a través de la red troncal de Microsoft; las VNets pueden estar en la misma región, en regiones distintas o en suscripciones distintas.

Permite:

- Conectar dos VNets de Azure entre sí con tráfico cifrado por IPsec
- Conectar VNets en distintas regiones o distintas suscripciones (cada VNet con su VPN Gateway y su Local network gateway apuntando a la otra)
- Combinar con conexiones S2S o P2S en el mismo gateway (según SKU y límites de conexiones)
- Sincronizar automáticamente rutas entre las VNets conectadas (sin BGP las rutas se aprenden por el túnel; con BGP se intercambian dinámicamente)

## Componentes

**VPN Gateway (cada VNet)** – Cada VNet debe tener su propio VPN Gateway en una GatewaySubnet; ambos gateways establecen el túnel entre sí

**Local network gateway (para VNet-to-VNet)** – En cada VNet se crea un Local network gateway que representa la otra VNet: se usa la IP pública del VPN Gateway de la otra VNet como "dirección IP del dispositivo VPN" y los espacios de direcciones de la otra VNet como "espacios de direcciones"

**Conexión VNet-to-VNet** – Conexión de tipo "VNet-to-VNet" que vincula el VPN Gateway de una VNet con el Local network gateway que apunta a la otra VNet (o conexión entre dos gateways usando el tipo VNet-to-VNet)

**Espacios de direcciones** – Las dos VNets no deben tener rangos de direcciones solapados para que el enrutamiento sea correcto

**Túnel IPsec** – El tráfico entre las VNets viaja cifrado por la red de Microsoft entre los dos VPN Gateways

## Funcionalidad

1. Se crea un VPN Gateway en la VNet 1 (GatewaySubnet) y otro en la VNet 2
2. En la VNet 1 se crea un Local network gateway con: "IP" = IP pública del VPN Gateway de la VNet 2, "espacios de direcciones" = address space de la VNet 2
3. En la VNet 2 se crea un Local network gateway con: "IP" = IP pública del VPN Gateway de la VNet 1, "espacios de direcciones" = address space de la VNet 1
4. Se crea una conexión VNet-to-VNet desde el gateway de la VNet 1 hacia el Local network gateway de la VNet 2 (y opcionalmente la conexión inversa si se desea redundancia o configuración explícita)
5. Los dos gateways establecen el túnel IPsec; el tráfico entre las VNets se enruta y cifra por el túnel
6. Las VNets pueden estar en la misma suscripción, en suscripciones distintas o en regiones distintas; los espacios de direcciones no deben solaparse
7. Opcionalmente se habilita BGP en ambas conexiones para enrutamiento dinámico entre las VNets

## Casos de Uso

- Conectar VNets en distintas regiones con tráfico cifrado (p. ej. redundancia geográfica con cifrado)
- Conectar VNets en distintas suscripciones cuando no se quiere o no se puede usar VNet peering
- Requerir cifrado IPsec explícito entre VNets (VNet peering no cifra; el tráfico va por la red de Microsoft pero sin túnel IPsec)
- Combinar conectividad VNet-to-VNet con S2S o P2S en el mismo gateway para topologías híbridas
- Crear topologías de red más complejas (hub-and-spoke con gateway en el hub y conexiones VNet-to-VNet a los spokes)

## Errores Comunes

- Confundir VNet-to-VNet con VNet peering: VNet-to-VNet usa dos VPN Gateways y túneles IPsec; el peering no usa gateway VPN y es conexión nativa de Azure (sin cifrado adicional)
- Definir espacios de direcciones solapados en las dos VNets (el enrutamiento fallaría; las VNets deben tener rangos distintos)
- En el Local network gateway de una VNet, poner la IP o los espacios de la misma VNet en lugar de la otra VNet (cada Local network gateway debe apuntar a la otra VNet)
- Pensar que con una sola conexión VNet-to-VNet (solo en un sentido) no hay conectividad (normalmente se crea la conexión en ambos sentidos o el tipo VNet-to-VNet crea ambos lados; revisar documentación según el flujo usado)
- Usar VNet-to-VNet cuando VNet peering sería suficiente y más simple (peering tiene menor latencia y no consume túneles del gateway; usar VPN VNet-to-VNet cuando se necesite cifrado o suscripciones/entidades distintas)

## Preguntas

1. ¿VPN VNet a VNet conecta dos redes virtuales de Azure mediante túneles IPsec entre dos VPN Gateways (uno en cada VNet)?

2. ¿Cada VNet debe tener su propio VPN Gateway para una conexión VNet-to-VNet?

3. ¿En cada VNet se crea un Local network gateway que apunta a la otra VNet (IP pública del gateway de la otra VNet y espacios de direcciones de la otra VNet)?

4. ¿Las dos VNets no deben tener espacios de direcciones solapados para que el enrutamiento funcione correctamente?

5. ¿VNet-to-VNet usa túneles IPsec (cifrado), mientras que VNet peering es conexión nativa de Azure sin gateway VPN?

6. ¿VNet-to-VNet puede conectar VNets en distintas regiones o distintas suscripciones?
