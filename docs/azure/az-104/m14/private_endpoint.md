# Private Endpoint

## Analogía

Un Private Endpoint es como tener una línea telefónica privada directa a un servicio que normalmente solo se puede llamar desde fuera. Imagina que vives en un edificio privado y quieres hablar con el banco que está en otro edificio. En lugar de salir a la calle y usar el teléfono público, tienes un teléfono interno que te conecta directamente con el banco como si estuviera en tu mismo edificio. Todo el tráfico permanece dentro de tu red privada, sin exponerse al exterior.

## Definición

Un Private Endpoint es una interfaz de red (NIC) que se despliega dentro de una Virtual Network (VNet) y proporciona conectividad privada a servicios PaaS de Azure.

Permite:

- Comunicación mediante IP privada dentro de la VNet
- Acceso a servicios PaaS sin salir al Internet público
- Tráfico que permanece en la red privada de Azure
- Acceso desde conexiones VPN y ExpressRoute mediante IP privada

## Componentes

**Network Interface Card (NIC)** – Tarjeta de Interfaz de red lógica asignada al Private Endpoint

**IP Privada** – Dirección IP privada asignada desde el espacio de direcciones de la VNet

**Private Link** – Servicio que conecta el Private Endpoint con el recurso PaaS

**DNS Zone** – Zona DNS privada que resuelve el nombre del servicio a la IP privada

## Funcionalidad

1. El Private Endpoint se crea dentro de una subred de la VNet
2. Se asigna una IP privada desde el rango de la VNet al Private Endpoint
3. El servicio PaaS se vincula al Private Endpoint mediante Private Link
4. El tráfico desde recursos en la VNet se dirige al Private Endpoint
5. La comunicación ocurre completamente dentro de la red privada de Azure
6. El servicio PaaS aparece como un recurso local dentro de la VNet

## Casos de Uso

- Conectar aplicaciones en VNet a Azure SQL Database de forma privada
- Acceder a Azure Storage desde recursos en red privada sin exposición pública
- Integrar servicios PaaS en arquitecturas con requisitos de seguridad estrictos
- Cumplir con requisitos de cumplimiento que requieren tráfico privado
- Reducir la superficie de ataque eliminando endpoints públicos

## Preguntas

1. ¿Un Private Endpoint permite que un recurso en una VNet acceda a un servicio PaaS usando una IP privada de la misma VNet?

2. ¿El tráfico entre un recurso en la VNet y un servicio PaaS a través de Private Endpoint sale al Internet público?

3. ¿Qué componente del Private Endpoint se encarga de resolver el nombre del servicio PaaS a su IP privada?

4. ¿Puede un Private Endpoint conectarse a servicios PaaS que están en diferentes regiones de Azure?

5. ¿Es necesario configurar una zona DNS privada para que funcione correctamente un Private Endpoint?
