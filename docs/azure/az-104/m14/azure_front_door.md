# Azure Front Door

## Analogía

Azure Front Door es como una red global de oficinas de correos que recibe paquetes de cualquier parte del mundo y los entrega rápidamente desde la oficina más cercana al destinatario. No solo reparte carga entre servidores (como un balanceador), sino que también acelera la entrega usando caché, protege contra ataques con un firewall integrado y puede enrutar el tráfico según la URL o el host. Opera globalmente en la capa de aplicación (HTTP/HTTPS) y está diseñado para aplicaciones modernas que necesitan alta disponibilidad, baja latencia y seguridad en todo el mundo.

## Definición

Azure Front Door es una red de entrega de contenido (CDN) global y equilibrador de carga de capa 7 (aplicación) que distribuye tráfico HTTP/HTTPS a aplicaciones y contenido estático/dinámico en múltiples regiones; proporciona aceleración global mediante caché, terminación SSL en el edge, enrutamiento inteligente, Web Application Firewall (WAF) integrado y protección DDoS; opera en más de 118 ubicaciones edge globales conectadas a Azure mediante una WAN privada.

Permite:

- Distribuir tráfico HTTP/HTTPS globalmente a backends en múltiples regiones de Azure o fuera de Azure
- Acelerar la entrega de contenido mediante caché en ubicaciones edge cercanas a los usuarios finales
- Enrutar tráfico según reglas basadas en path (URL), host, headers o geolocalización
- Terminar SSL/TLS en el edge con certificados gestionados automáticamente (renovación automática)
- Proteger aplicaciones con Web Application Firewall (WAF) integrado contra ataques OWASP, SQL injection, XSS y DDoS de capa 7
- Proporcionar alta disponibilidad mediante health probes y failover automático entre backends
- Operar en capa 7: inspeccionar y modificar headers, path, host y contenido HTTP/HTTPS
- Integrar con otros servicios de Azure (App Service, Storage, etc.) y endpoints externos

## Componentes

**Front Door Profile** – Recurso que contiene la configuración de endpoints, dominios, origin groups, routes y políticas de seguridad

**Endpoint** – Punto de entrada global con un dominio (p. ej. `contoso.azurefd.net` o dominio personalizado); puede tener múltiples rutas

**Route** – Regla que asocia un dominio/path con un origin group y define cómo se enruta el tráfico; puede tener condiciones (path, host, headers) y acciones (rewrite, redirect, cache)

**Origin Group** – Conjunto de backends (origins) que reciben el tráfico; puede incluir VMs, App Services, Storage Accounts, o cualquier endpoint HTTP/HTTPS; se configuran health probes y pesos para distribución

**Origin** – Backend individual (IP, FQDN o recurso de Azure) que sirve el contenido; puede estar en Azure o fuera de Azure

**Web Application Firewall (WAF)** – Política de seguridad integrada que protege contra vulnerabilidades OWASP, SQL injection, cross-site scripting (XSS) y ataques DDoS de capa 7; puede operar en modo detección o prevención

**Health Probe** – Sonda que comprueba periódicamente si los origins están sanos; si un origin falla, el tráfico se redirige automáticamente a otros origins sanos en el grupo

**Caché** – Almacenamiento de contenido estático en ubicaciones edge para reducir latencia y carga en los origins; se configura por ruta con reglas de TTL y condiciones

**Terminación SSL/TLS** – Descifrado de tráfico HTTPS en el edge; certificados gestionados automáticamente con renovación; soporta end-to-end TLS si se requiere

**Capa 7 (aplicación)** – Nivel del modelo OSI en el que opera; entiende HTTP/HTTPS, URL, host, headers y puede modificar solicitudes/respuestas

## Funcionalidad

1. Se crea un Front Door Profile en Azure (recurso global, no ligado a una región específica)
2. Se configura un endpoint con un dominio (Azure FD o personalizado) y se asocia un certificado SSL si es HTTPS
3. Se crean origin groups con uno o más origins (backends) y se configuran health probes para monitoreo
4. Se crean rutas que asocian dominios/paths con origin groups; se pueden definir condiciones (path matching, host matching) y acciones (cache, rewrite, redirect)
5. Opcionalmente se configura WAF con reglas gestionadas o personalizadas (modo detección o prevención)
6. El Front Door recibe solicitudes HTTP/HTTPS de usuarios globales y las enruta a la ubicación edge más cercana
7. Si el contenido está en caché y es válido, se sirve desde el edge; si no, se obtiene del origin y se cachea
8. El WAF inspecciona el tráfico y bloquea o registra amenazas según las reglas configuradas
9. Si un origin falla el health probe, el tráfico se redirige automáticamente a otros origins sanos en el grupo

## Casos de Uso

- Aplicaciones web globales que necesitan baja latencia para usuarios distribuidos mundialmente
- Contenido estático y dinámico que se beneficia de caché en ubicaciones edge cercanas a los usuarios
- Aplicaciones que requieren alta disponibilidad con failover automático entre múltiples regiones
- Protección de aplicaciones web contra ataques comunes (OWASP, SQL injection, XSS) con WAF integrado
- Enrutamiento global inteligente según geolocalización, path o host a diferentes backends
- Terminación SSL centralizada con certificados gestionados automáticamente
- Escenarios híbridos: backends en Azure y fuera de Azure (on-premises, otras nubes)

## Errores Comunes

- Confundir Front Door con Application Gateway (Front Door es global, CDN, múltiples regiones; Application Gateway es regional, dentro de una VNet)
- Confundir Front Door con Traffic Manager (Front Door opera en capa 7, HTTP/HTTPS, con caché y WAF; Traffic Manager opera en DNS, capa 4, sin inspección de contenido)
- Creer que Front Door requiere VNet (no requiere VNet; opera globalmente en el edge)
- Esperar que Front Door equilibre carga TCP/UDP que no sea HTTP/HTTPS (solo soporta HTTP/HTTPS/WebSockets)
- Olvidar configurar health probes correctamente (si fallan, los origins pueden marcarse como no sanos incorrectamente)
- No entender que Front Door es un servicio global (no está ligado a una región específica de Azure)

## Preguntas

1. ¿Azure Front Door es una red CDN global y equilibrador de carga de capa 7 que distribuye tráfico HTTP/HTTPS a aplicaciones en múltiples regiones?

2. ¿Front Door puede acelerar la entrega de contenido mediante caché en ubicaciones edge cercanas a los usuarios finales?

3. ¿Front Door puede proteger aplicaciones con Web Application Firewall (WAF) integrado contra ataques OWASP, SQL injection y XSS?

4. ¿Front Door puede enrutar tráfico según reglas basadas en path (URL), host o geolocalización a diferentes origin groups?

5. ¿Front Door puede terminar SSL/TLS en el edge con certificados gestionados automáticamente y renovación automática?

6. ¿Front Door opera globalmente en más de 118 ubicaciones edge y no requiere una VNet para funcionar?
