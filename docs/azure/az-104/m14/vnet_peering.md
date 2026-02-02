# VNet Peering

VNet peering es como unir dos barrios privados con un puente directo: el tráfico entre ambos va por la red de Microsoft (no por Internet) y no necesitas una puerta de enlace VPN. Cada barrio sigue teniendo su propio espacio de direcciones y no pueden solaparse. Puede ser en la misma región (peering regional) o entre regiones (peering global).

## Definición

VNet peering es la conexión nativa entre dos redes virtuales de Azure que permite que el tráfico entre ellas fluya por la red troncal de Microsoft; no usa VPN Gateway ni cifrado IPsec; los espacios de direcciones de las dos VNets no deben solaparse; el peering no es transitivo (si A-B y B-C están emparejados, A y C no se ven a menos que A-C también esté emparejado).

Permite:

- Conectar dos VNets (misma región o regiones distintas) sin gateway VPN.
- Tráfico de baja latencia y alto throughput por la red de Microsoft.
- Espacios de direcciones distintos y no solapados en cada VNet.
- Opcionalmente permitir tránsito de gateway (usar el VPN/ExpressRoute Gateway de la VNet emparejada).

## Componentes

**Peering regional** – Peering entre dos VNets en la misma región de Azure.

**Peering global** – Peering entre dos VNets en regiones distintas de Azure.

**Peering en un sentido** – Cada peering se configura en ambas VNets (desde A hacia B y desde B hacia A) para que el tráfico fluya en ambos sentidos; en el portal a menudo se puede crear “peering en un clic” que crea ambos lados.

**Espacios de direcciones** – Las dos VNets deben tener address spaces que no se solapen; si se añaden o modifican rangos en una VNet emparejada, puede ser necesario sincronizar el peering.

**No transitividad** – Si VNet A está emparejada con B y B con C, A no puede alcanzar C a través de B solo con peering; hace falta peering A-C o usar tránsito de gateway (si B tiene un gateway y se permite “gateway transit”).

**Gateway transit** – Opción para permitir que una VNet use el VPN o ExpressRoute Gateway de la VNet emparejada (p. ej. en topología hub-and-spoke, los spokes pueden usar el gateway del hub).

**Límites** – Una VNet puede tener un número máximo de peerings (p. ej. 500 por defecto; con Virtual Network Manager puede aumentarse).

## Funcionalidad

1. Se crean dos VNets con espacios de direcciones que no se solapan (misma región o regiones distintas).
2. Se crea el peering: desde la VNet A se añade un peering hacia la VNet B (y desde B hacia A si no se usa “peering en un clic”).
3. Una vez conectado, los recursos de una VNet pueden alcanzar los recursos de la otra por IP privada (si no hay NSG u otras reglas que lo impidan).
4. El tráfico va por la red troncal de Microsoft; no sale a Internet ni usa VPN Gateway.
5. Opcionalmente se habilita “Allow gateway transit” en una VNet y “Use remote gateways” en la otra para que una use el gateway de la otra.
6. Si se modifican los address spaces de una VNet emparejada, puede ser necesario sincronizar el peering para que las rutas se actualicen.
7. El peering no es transitivo: para conectividad A → B → C hace falta peering A-C o tránsito de gateway según el diseño.

## Casos de Uso

- Conectar VNets en la misma región (p. ej. front-end y back-end en VNets separadas) sin gateway VPN.
- Conectar VNets en distintas regiones (peering global) para redundancia o datos cercanos al usuario.
- Topología hub-and-spoke: hub con gateway y spokes emparejados al hub con “Use remote gateways” para usar el gateway del hub.
- Evitar VPN Gateway cuando no se necesita cifrado IPsec entre VNets (menor latencia y menor costo que VNet-to-VNet).
- Aislar cargas de trabajo en VNets distintas y permitir solo el tráfico necesario mediante peering y NSG.

## Errores Comunes

- Creer que el peering es transitivo (A emparejada con B y B con C no implica que A llegue a C; hace falta peering A-C o tránsito de gateway).
- Definir espacios de direcciones solapados entre las dos VNets (el peering no se puede establecer si hay solapamiento).
- Confundir peering con VPN VNet-to-VNet (peering no usa gateway VPN ni cifrado IPsec; es conexión nativa de Azure).
- Pensar que con un solo peering “desde A hacia B” basta (normalmente se necesita el peering en ambos lados para tráfico bidireccional; el portal puede crearlo en un solo paso).
- Olvidar que al cambiar el address space de una VNet emparejada puede ser necesario sincronizar el peering.

## Preguntas

1. ¿VNet peering conecta dos redes virtuales de Azure por la red troncal de Microsoft sin usar VPN Gateway?.

2. ¿Los espacios de direcciones de las dos VNets emparejadas no deben solaparse?.

3. ¿El peering no es transitivo: si A está emparejada con B y B con C, A no alcanza C a través de B solo por peering?.

4. ¿Peering global conecta VNets en distintas regiones de Azure?.

5. ¿Se puede permitir “gateway transit” para que una VNet use el VPN o ExpressRoute Gateway de la VNet emparejada?.

6. ¿VNet peering no usa cifrado IPsec a diferencia de VPN VNet-to-VNet?.
