# Azure Traffic Manager

## Analogía

Azure Traffic Manager es como un directorio telefónico inteligente que, cuando alguien pregunta por un número, decide qué número dar según dónde esté la persona que pregunta y qué números estén disponibles. Opera a nivel de DNS: cuando un usuario busca tu aplicación, Traffic Manager responde con la IP del servidor más adecuado según el método de enrutamiento configurado (más cercano, más rápido, con failover, etc.). No ve el tráfico real; solo responde consultas DNS para dirigir a los usuarios al endpoint correcto.

## Definición

Azure Traffic Manager es un equilibrador de carga basado en DNS que distribuye tráfico a endpoints públicos (aplicaciones, servicios) en múltiples regiones de Azure o fuera de Azure; opera a nivel de DNS (no ve el tráfico real) y utiliza métodos de enrutamiento para determinar qué IP devolver en la respuesta DNS; proporciona alta disponibilidad mediante health monitoring y failover automático cuando un endpoint falla.

Permite:

- Distribuir tráfico a endpoints en múltiples regiones de Azure o fuera de Azure (on-premises, otras nubes)
- Enrutar tráfico según seis métodos: Priority (failover), Weighted (distribución por peso), Performance (menor latencia), Geographic (por ubicación geográfica), Multivalue (múltiples IPs sanas), Subnet (por subred origen)
- Proporcionar alta disponibilidad mediante health monitoring de endpoints y failover automático cuando un endpoint falla
- Realizar mantenimiento sin downtime dirigiendo tráfico a endpoints alternativos
- Combinar métodos de enrutamiento mediante perfiles anidados (nested profiles) para reglas complejas
- Operar a nivel DNS: no ve el tráfico real, solo responde consultas DNS con la IP del endpoint adecuado

## Componentes

**Traffic Manager Profile** – Recurso que contiene la configuración del método de enrutamiento, endpoints y health monitoring; tiene un nombre DNS único (p. ej. `contoso.trafficmanager.net`)

**Endpoint** – Destino al que Traffic Manager puede dirigir tráfico; puede ser Azure (App Service, Public IP, Load Balancer) o externo (IP, FQDN); cada endpoint tiene un estado (Enabled/Disabled) y un peso (para Weighted)

**Método de enrutamiento (routing method)** – Algoritmo que determina qué endpoint se devuelve en la respuesta DNS; seis métodos disponibles: Priority, Weighted, Performance, Geographic, Multivalue, Subnet

**Priority (Prioridad)** – Método de enrutamiento que dirige todo el tráfico al endpoint con prioridad más alta (menor número); si falla, se usa el siguiente en orden de prioridad; ideal para failover

**Weighted (Ponderado)** – Método que distribuye tráfico según pesos asignados a cada endpoint; pesos iguales distribuyen tráfico uniformemente; útil para distribución gradual o pruebas A/B

**Performance (Rendimiento)** – Método que dirige usuarios al endpoint geográficamente más cercano según la latencia de red; Traffic Manager mantiene una tabla de latencias entre ubicaciones

**Geographic (Geográfico)** – Método que dirige tráfico según la ubicación geográfica de la consulta DNS (país/región); útil para cumplimiento de soberanía de datos o localización

**Multivalue (Múltiples valores)** – Método que devuelve múltiples endpoints sanos (hasta 10) en la respuesta DNS; el cliente elige cuál usar; solo para endpoints con direcciones IPv4/IPv6

**Subnet (Subred)** – Método que dirige tráfico según la subred origen de la consulta DNS; útil para dirigir tráfico de oficinas específicas a endpoints dedicados

**Health Monitoring** – Sondas HTTP/HTTPS que comprueban periódicamente si los endpoints están sanos; si un endpoint falla, se elimina de las respuestas DNS hasta que recupere la salud

**Nested Profiles (Perfiles anidados)** – Combinación de múltiples perfiles de Traffic Manager para crear reglas de enrutamiento complejas; un perfil padre puede tener otros perfiles como endpoints

## Funcionalidad

1. Se crea un Traffic Manager Profile en Azure con un método de enrutamiento seleccionado (Priority, Weighted, Performance, Geographic, Multivalue o Subnet)
2. Se añaden endpoints al perfil (Azure o externos) y se configuran propiedades según el método (prioridad, peso, región geográfica, subred, etc.)
3. Se configura health monitoring: protocolo (HTTP/HTTPS), puerto, path y intervalo de sondeo
4. Traffic Manager responde a consultas DNS con el nombre del perfil (p. ej. `contoso.trafficmanager.net`)
5. Cuando se recibe una consulta DNS, Traffic Manager evalúa el método de enrutamiento y devuelve la IP del endpoint adecuado
6. Health monitoring comprueba periódicamente cada endpoint; si falla, se elimina de las respuestas DNS
7. El cliente resuelve el DNS y se conecta directamente al endpoint (Traffic Manager no ve el tráfico real)
8. Opcionalmente se pueden crear perfiles anidados para combinar métodos de enrutamiento

## Casos de Uso

- Failover entre regiones: dirigir todo el tráfico a una región primaria y conmutar automáticamente a una secundaria si falla (Priority)
- Distribución de carga entre múltiples regiones según pesos configurados (Weighted)
- Mejorar rendimiento dirigiendo usuarios al endpoint con menor latencia según su ubicación (Performance)
- Cumplimiento de soberanía de datos: dirigir tráfico de países específicos a endpoints en esas regiones (Geographic)
- Escenarios híbridos: dirigir tráfico a aplicaciones en Azure y on-premises según la ubicación o prioridad
- Mantenimiento sin downtime: deshabilitar temporalmente un endpoint y dirigir tráfico a alternativos

## Errores Comunes

- Confundir Traffic Manager con Load Balancer o Application Gateway (Traffic Manager opera en DNS, no ve tráfico real; los otros operan en capa 4 o 7)
- Confundir Traffic Manager con Front Door (Traffic Manager es DNS, sin caché ni WAF; Front Door es CDN global con caché y WAF)
- Creer que Traffic Manager puede enrutar por URL o path (no puede; solo opera en DNS; para enrutamiento por URL se usa Application Gateway o Front Door)
- Esperar que Traffic Manager equilibre carga dentro de una región (no está diseñado para eso; se usa Load Balancer o Application Gateway)
- No entender que Traffic Manager no ve el tráfico real (solo responde DNS; el cliente se conecta directamente al endpoint)
- Configurar health probes incorrectamente (si el path o puerto no coinciden, los endpoints pueden marcarse como no sanos)

## Preguntas

1. ¿Azure Traffic Manager es un equilibrador de carga basado en DNS que distribuye tráfico a endpoints públicos en múltiples regiones?

2. ¿Traffic Manager puede enrutar tráfico según seis métodos: Priority (failover), Weighted, Performance, Geographic, Multivalue y Subnet?

3. ¿Traffic Manager proporciona alta disponibilidad mediante health monitoring y failover automático cuando un endpoint falla?

4. ¿Traffic Manager opera solo a nivel DNS y no ve el tráfico real (el cliente se conecta directamente al endpoint después de resolver el DNS)?

5. ¿El método Priority dirige todo el tráfico al endpoint con prioridad más alta y conmuta automáticamente si falla?

6. ¿El método Performance dirige usuarios al endpoint geográficamente más cercano según la latencia de red?
