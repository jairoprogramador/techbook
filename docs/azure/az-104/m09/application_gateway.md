# Azure Application Gateway

## Analogía

Azure Application Gateway es como el portero de un edificio que no solo reparte visitas entre varias oficinas, sino que decide a qué oficina enviar a cada persona según la URL o el nombre del host: "si piden /api, a los servidores de API; si piden /tienda, a los de la tienda". Puede terminar el SSL (descifrar en la puerta y hablar en claro con los servidores internos), aplicar un firewall de aplicaciones web (WAF) y mantener la sesión del usuario en el mismo servidor. Opera en capa 7 (HTTP/HTTPS), así que entiende URLs, headers y contenido web. Sirve para aplicaciones web y APIs que necesitan enrutamiento inteligente, SSL o protección WAF.

## Definición

Azure Application Gateway es un equilibrador de carga de capa 7 (aplicación) que distribuye tráfico HTTP y HTTPS entre backends (VMs, VM Scale Sets, etc.); inspecciona el contenido de la solicitud (URL, host, headers) y permite enrutamiento por path, por host, terminación SSL, afinidad de sesión basada en cookies y Web Application Firewall (WAF).

Permite:

- Distribuir tráfico HTTP/HTTPS entre varias VMs o instancias de un VM Scale Set (grupo de backends)
- Operar en capa 7: inspeccionar host, path (URL) y headers para enrutar a distintos backends según reglas
- Enrutamiento basado en path (p. ej. /api → pool de API, /tienda → pool de tienda) o en host (p. ej. api.dominio.com → pool de API)
- Terminación SSL en el Application Gateway: el cliente habla HTTPS con el gateway y el gateway puede hablar HTTP o HTTPS con los backends
- Gestionar certificados SSL en el gateway (renovación, múltiples sitios)
- Web Application Firewall (WAF) para proteger contra vulnerabilidades OWASP y patrones maliciosos
- Afinidad de sesión basada en cookies para que las peticiones de un usuario vayan al mismo backend
- Integrar con VM Scale Sets para distribuir tráfico entre instancias

## Componentes

**Frontend** – Configuración del lado que recibe el tráfico: una o más direcciones IP (pública o privada) y puertos (80, 443); puede tener varios listeners (HTTP/HTTPS)

**Listener** – Escucha en un puerto y protocolo (HTTP o HTTPS); si es HTTPS, se asocia un certificado SSL para terminación en el gateway

**Regla de enrutamiento (routing rule)** – Asocia un listener con un backend pool y opcionalmente con condiciones (path, host); determina a qué pool se envía cada solicitud según la URL o el host

**Enrutamiento por path (path-based routing)** – Envío de solicitudes a distintos backend pools según el path de la URL (p. ej. /api/* → pool API, /imagenes/* → pool de imágenes)

**Enrutamiento por host (multi-site)** – Envío de solicitudes a distintos backend pools según el header Host (p. ej. api.dominio.com → pool API, www.dominio.com → pool web)

**Backend pool** – Conjunto de destinos (IPs, FQDN, NICs de VMs o VM Scale Set) que reciben el tráfico según las reglas de enrutamiento

**Terminación SSL** – Descifrado del tráfico HTTPS en el Application Gateway; el gateway puede reenviar al backend en HTTP o reencriptar (end-to-end SSL)

**Web Application Firewall (WAF)** – SKU o modo del Application Gateway que inspecciona el tráfico HTTP/HTTPS y bloquea o registra solicitudes que coincidan con reglas OWASP o personalizadas

**Health probe** – Comprueba periódicamente si los backends responden (HTTP/HTTPS); si un backend no responde, se deja de enviar tráfico hasta que vuelva a estar sano

**Capa 7 (aplicación)** – Nivel del modelo OSI en el que opera; entiende HTTP/HTTPS, URL, host y headers; permite decisiones de enrutamiento basadas en el contenido

## Funcionalidad

1. Se crea un recurso Application Gateway en una VNet (subred dedicada para el gateway)
2. Se configura el frontend: IP pública o privada y listeners (HTTP en puerto 80, HTTPS en puerto 443 con certificado)
3. Se crean uno o más backend pools (VMs, VM Scale Sets, IPs o FQDN)
4. Se configuran reglas de enrutamiento: listener → backend pool, con opcionales condiciones por path o host (path-based, multi-site)
5. Se configura un health probe (HTTP/HTTPS) para comprobar el estado de los backends
6. Opcionalmente se habilita WAF y se configuran reglas de detección o prevención
7. El Application Gateway recibe solicitudes HTTP/HTTPS, aplica terminación SSL si corresponde, evalúa path/host según las reglas y envía la solicitud al backend pool correspondiente
8. Opcionalmente se configura afinidad de sesión por cookies para que el mismo cliente vaya al mismo backend

## Casos de Uso

- Aplicaciones web o APIs que necesitan enrutamiento por URL (path) o por dominio (host) a distintos backends
- Terminación SSL en un único punto (certificados en el gateway, backends en HTTP o HTTPS)
- Protección de aplicaciones web con Web Application Firewall (WAF) contra OWASP y ataques comunes
- Varios sitios (multi-site) en el mismo Application Gateway con distintos backend pools según el host
- Afinidad de sesión para aplicaciones que requieren que un usuario mantenga la misma instancia backend
- Integración con VM Scale Sets para equilibrar carga HTTP/HTTPS entre instancias con enrutamiento inteligente

## Errores Comunes

- Confundir Application Gateway con Load Balancer (Application Gateway es capa 7, HTTP/HTTPS, con path/host routing, SSL y WAF; Load Balancer es capa 4, TCP/UDP, sin inspección de contenido)
- Usar Application Gateway para tráfico TCP/UDP que no sea HTTP/HTTPS (Application Gateway solo soporta HTTP/HTTPS/WebSockets; para TCP/UDP puro se usa Load Balancer)
- Creer que el Application Gateway y el Load Balancer hacen lo mismo (el primero entiende URL y host; el segundo solo puerto y protocolo)
- Configurar reglas de enrutamiento por path sin tener en cuenta el orden de evaluación (la primera regla que coincida suele aplicarse)
- Olvidar que Application Gateway requiere una subred dedicada (no se pueden desplegar otras cargas en la misma subred)

## Preguntas

1. ¿Azure Application Gateway opera en capa 7 (HTTP/HTTPS) y puede enrutar tráfico según path (URL) o host?

2. ¿Application Gateway puede realizar terminación SSL (descifrar en el gateway y reenviar al backend en HTTP o HTTPS)?

3. ¿El enrutamiento por path permite enviar solicitudes a distintos backend pools según la URL (p. ej. /api → pool API)?

4. ¿Web Application Firewall (WAF) en Application Gateway protege contra vulnerabilidades OWASP y patrones maliciosos en tráfico HTTP/HTTPS?

5. ¿Application Gateway solo soporta tráfico HTTP/HTTPS (y WebSockets), a diferencia de Load Balancer que soporta TCP/UDP?

6. ¿Application Gateway requiere una subred dedicada para su despliegue?
