# Rutas definidas por el usuario (UDR)

Las rutas definidas por el usuario (UDR) son como indicar en un cruce: “todo el tráfico que vaya a este destino no sigas la calle por defecto, sal por esta otra”. Azure ya pone rutas por defecto (entre subredes, a Internet, etc.). Si quieres que cierto tráfico (p. ej. todo lo que va a Internet) pase por un firewall (appliance de seguridad) en vez de salir directo, creas una tabla de rutas con una ruta que dice “para 0.0.0.0/0 el próximo salto es la IP del firewall” y asocias esa tabla a la subred. Así el tráfico se fuerza por el appliance.

## Definición

Las rutas definidas por el usuario (User-Defined Routes, UDR) son rutas personalizadas en una tabla de rutas de Azure que sobrescribe el enrutamiento por defecto del sistema; la tabla de rutas se asocia a una o más subredes y cada ruta define un prefijo de destino y un próximo salto (Virtual Appliance, VPN Gateway, Internet, None, etc.).

Permite:

- Enviar tráfico con un destino concreto (p. ej. 0.0.0.0/0) a un próximo salto distinto del predeterminado (p. ej. una VM que actúa como firewall).
- Implementar topologías hub-and-spoke donde el tráfico de los spokes pasa por un hub (firewall o NVA).
- Forzar tráfico a Internet por un túnel (forced tunneling) usando el próximo salto “VPN Gateway”.
- Descartar tráfico hacia ciertos destinos usando el próximo salto “None”.
- Las rutas del sistema siguen existiendo; las rutas de la tabla de usuario tienen prioridad sobre ellas cuando coinciden el prefijo.

## Componentes

**Tabla de rutas (route table)** – Recurso de Azure que contiene una lista de rutas; se asocia a subredes (una subred puede tener una sola tabla de rutas).

**Ruta (route)** – Regla con nombre: prefijo de dirección (p. ej. 10.0.0.0/16, 0.0.0.0/0) y tipo de próximo salto.

**Próximo salto (next hop type)** – Destino del tráfico que coincide con el prefijo: Virtual Appliance (IP de una VM/NVA), VNet Gateway (VPN o ExpressRoute), Internet, None (descartar), VNet local (obsoleto en ARM), etc.

**Virtual Appliance** – Próximo salto que apunta a una IP (normalmente una VM o NVA en la VNet) que enruta o filtra el tráfico (firewall, proxy).

**Asociación a subred** – La tabla de rutas se asocia a una o más subredes; todas las VM de esa subred usan las rutas de la tabla para decidir el próximo salto.

**Rutas del sistema** – Rutas que Azure crea por defecto (tráfico entre subredes, a Internet, etc.); no se eliminan; las UDR las sobrescriben cuando el prefijo coincide (la ruta más específica gana).

## Funcionalidad

1. Se crea una tabla de rutas en la VNet (y opcionalmente en una región concreta).
2. Se añaden rutas: nombre, prefijo de destino (p. ej. 0.0.0.0/0), próximo salto (Virtual Appliance con IP del firewall, o VNet Gateway, o Internet, o None).
3. Se asocia la tabla de rutas a una o más subredes.
4. Las VM de esas subredes usan la tabla de rutas para enrutar; cuando un paquete coincide con el prefijo de una ruta UDR, se usa el próximo salto definido en lugar del comportamiento por defecto.
5. Para “Virtual Appliance” la IP debe ser alcanzable (VM en la VNet, normalmente en una subred dedicada); la VM debe tener IP forwarding habilitado si va a reenviar tráfico.
6. Las rutas del sistema siguen aplicando para destinos que no coinciden con ninguna UDR.
7. Si dos rutas coinciden en prefijo, gana la más específica (prefijo más largo).

## Casos de Uso

- Forzar todo el tráfico a Internet (0.0.0.0/0) por un firewall (NVA) en la VNet: ruta con próximo salto Virtual Appliance = IP del firewall.
- Topología hub-and-spoke: en los spokes, ruta 0.0.0.0/0 (o rangos concretos) con próximo salto la IP del firewall en el hub.
- Forced tunneling: ruta 0.0.0.0/0 con próximo salto VNet Gateway para que el tráfico a Internet salga por el túnel VPN/ExpressRoute.
- Descartar tráfico a ciertos rangos: ruta con prefijo y próximo salto None.
- Enrutar tráfico a una red local concreta por una VM que hace de router: ruta con prefijo de la red local y próximo salto Virtual Appliance.

## Errores Comunes

- Creer que una subred puede tener varias tablas de rutas (una subred tiene una sola tabla de rutas asociada).
- Usar próximo salto Virtual Appliance sin habilitar IP forwarding en la NIC de la VM (la VM no reenviará el tráfico).
- Poner la IP del appliance en una subred a la que no se puede llegar por las rutas existentes (el tráfico no llegará al appliance).
- Confundir UDR con NSG (UDR cambia el próximo salto del enrutamiento; NSG filtra tráfico permitiendo o denegando; ambos pueden aplicarse).
- Definir una ruta 0.0.0.0/0 hacia un appliance sin tener reglas NSG que permitan el tráfico hacia y desde esa IP (el NSG puede bloquear).

## Preguntas

1. ¿Las rutas definidas por el usuario (UDR) override el enrutamiento por defecto de Azure cuando el prefijo de destino coincide?.

2. ¿La tabla de rutas se asocia a una o más subredes y cada subred puede tener solo una tabla de rutas?.

3. ¿El próximo salto “Virtual Appliance” envía el tráfico a una IP (p. ej. un firewall/NVA) que debe ser alcanzable desde la subred?.

4. ¿Para que una VM actúe como appliance (reenvíe tráfico) debe tener IP forwarding habilitado en la NIC?.

5. ¿La ruta 0.0.0.0/0 con próximo salto VNet Gateway se usa para forced tunneling (todo el tráfico a Internet por el túnel)?.

6. ¿Las rutas del sistema de Azure no se eliminan y las UDR tienen prioridad cuando el prefijo coincide?.
