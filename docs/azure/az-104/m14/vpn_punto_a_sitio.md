# VPN Punto a Sitio (Point-to-Site, P2S)

VPN punto a sitio es como dar a cada empleado una llave temporal para entrar al edificio desde casa: cada uno se conecta desde su propio dispositivo (portátil, móvil) a la red de la empresa en Azure mediante un túnel cifrado. No hace falta un dispositivo VPN en la oficina del empleado; solo el cliente VPN en su equipo y las credenciales (certificado, Entra ID o RADIUS). La puerta de enlace que recibe las conexiones es el VPN Gateway de la VNet. Ideal para teletrabajo o acceso puntual sin desplegar una conexión sitio a sitio.

## Definición

VPN punto a sitio (P2S) es una conexión VPN desde un cliente individual (ordenador o dispositivo) a una red virtual de Azure; el tráfico va cifrado entre el cliente y el VPN Gateway de la VNet; no requiere un dispositivo VPN en el lado del cliente ni una IP pública fija en el cliente; soporta autenticación por certificado, Microsoft Entra ID o RADIUS.

Permite:

- Conectar usuarios remotos (teletrabajo, desarrolladores, soporte) a la VNet desde su dispositivo
- No requerir dispositivo VPN ni IP pública en el lado del cliente; solo el cliente VPN y credenciales
- Usar autenticación por certificado (raíz + cliente), Microsoft Entra ID o RADIUS (incluyendo MFA)
- Elegir protocolo: OpenVPN, IKEv2 o SSTP (Windows) según sistema operativo y requisitos
- Asignar a los clientes un rango de direcciones IP desde un pool de la VNet (Address pool P2S)

## Componentes

**Cliente VPN** – Aplicación o cliente integrado en el sistema operativo (Azure VPN Client, cliente integrado Windows, etc.) que establece el túnel P2S hacia el VPN Gateway

**Address pool (grupo de direcciones P2S)** – Rango de direcciones IP (p. ej. 10.4.0.0/24) que el gateway asigna a los clientes conectados; debe no solaparse con la VNet ni con redes locales conectadas

**Autenticación por certificado** – Certificado raíz cargado en el gateway y certificado de cliente instalado en cada dispositivo; el gateway valida el certificado del cliente contra la raíz

**Autenticación con Microsoft Entra ID** – El usuario inicia sesión con su identidad de Entra ID; el gateway valida el token; compatible con OpenVPN; permite MFA y conditional access

**Autenticación RADIUS** – Servidor RADIUS (local o en Azure) que valida credenciales; permite integrar con MFA o directorios locales

**Protocolos P2S** – OpenVPN (multiplataforma), IKEv2 (multiplataforma, reconexión rápida), SSTP (solo Windows, puerto 443)

**VPN Gateway** – Recurso en la VNet que termina las conexiones P2S; debe tener tipo VPN y configuración P2S habilitada

## Funcionalidad

1. Se crea un VPN Gateway en la VNet (subred GatewaySubnet) con tipo VPN
2. Se configura la conexión P2S en el gateway: se define el address pool (rango de IPs para clientes) y el método de autenticación (certificado, Entra ID o RADIUS)
3. Según el método: se cargan certificados raíz y se generan certificados de cliente; o se configura Entra ID; o se configura el servidor RADIUS
4. Se genera y descarga el perfil de cliente VPN (archivo de configuración con el punto de terminación, protocolo, etc.)
5. Se instala el perfil en cada dispositivo (o se distribuye el Azure VPN Client con el perfil)
6. El usuario inicia la conexión VPN, se autentica (certificado, Entra ID o RADIUS) y recibe una IP del address pool
7. El tráfico entre el cliente y los recursos de la VNet viaja cifrado por el túnel P2S
8. P2S puede coexistir con conexiones S2S y VNet-to-VNet en el mismo gateway (según SKU y límites)

## Casos de Uso

- Dar acceso remoto a desarrolladores o soporte a VMs y recursos dentro de la VNet sin exponerlos a Internet
- Teletrabajo: empleados se conectan desde casa a la red corporativa en Azure con Entra ID y MFA
- Pruebas o acceso puntual sin desplegar una VPN sitio a sitio
- Usar RADIUS para integrar con directorio local o MFA existente
- Elegir OpenVPN o IKEv2 para clientes multiplataforma (Windows, macOS, Linux, iOS, Android)

## Errores Comunes

- Confundir P2S con S2S: P2S es cliente a VNet (un dispositivo); S2S es red local a VNet (dispositivo VPN en sede)
- Pensar que P2S requiere una IP pública fija en el cliente (no la requiere; el cliente puede estar detrás de NAT)
- Creer que forced tunneling del gateway aplica al tráfico de clientes P2S (forced tunneling es para S2S; el tráfico P2S se enruta según la configuración del cliente y del perfil)
- Usar un address pool P2S que se solape con el espacio de direcciones de la VNet o con redes conectadas (debe ser un rango distinto)
- Olvidar que SSTP solo funciona en clientes Windows; para otros sistemas hay que usar OpenVPN o IKEv2

## Preguntas

1. ¿VPN punto a sitio (P2S) permite que un cliente individual (ordenador o dispositivo) se conecte a una VNet de Azure mediante un túnel cifrado sin dispositivo VPN en el lado del cliente?

2. ¿P2S soporta autenticación por certificado, Microsoft Entra ID y RADIUS?

3. ¿El address pool (grupo de direcciones P2S) es el rango de IPs que el gateway asigna a los clientes conectados y no debe solaparse con la VNet?

4. ¿OpenVPN e IKEv2 son protocolos P2S multiplataforma, mientras que SSTP solo está soportado en clientes Windows?

5. ¿La autenticación con Entra ID en P2S permite usar MFA y conditional access?

6. ¿P2S y S2S pueden coexistir en el mismo VPN Gateway (según SKU y límites)?
