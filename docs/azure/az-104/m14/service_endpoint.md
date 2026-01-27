# Endpoint de Servicio

## Analogía

Un Endpoint de Servicio es como tener un carril exclusivo en la autopista que te lleva directamente a un destino específico, pero sigues usando la autopista pública del lugar. Imagina que quieres ir a un almacén que tiene una dirección pública, pero en lugar de tomar todas las calles normales con semáforos, tienes un carril rápido que te lleva directamente. El almacén sigue teniendo su dirección pública, pero tú llegas más rápido y de forma más segura por el carril privado. El almacén solo abre la puerta para ti porque sabe que vienes por el carril seguro.

## Definición

Un Endpoint de Servicio es una regla de enrutamiento que optimiza el tráfico desde una subred de una Virtual Network hacia servicios PaaS de Azure, enrutándolo a través de la red privada de Microsoft.

Permite:

- Tráfico optimizado que viaja por la red privada de Azure
- Uso de la IP pública del servicio PaaS
- Restricción de acceso mediante reglas de firewall del servicio
- El servicio no se introduce dentro de la VNet
- Acceso completo a todas las funcionalidades del servicio PaaS

## Componentes

**Subred** – Subred de la VNet donde se habilita el Service Endpoint

**Regla de Enrutamiento** – Regla que optimiza el tráfico hacia el servicio PaaS

**Firewall del Servicio** – Regla que permite tráfico desde la VNet específica

**IP Pública del Servicio** – Dirección pública que se usa para acceder al servicio

## Funcionalidad

1. Se habilita un Endpoint de Servicio en una subred específica de la VNet
2. Se configura la regla de firewall en el servicio PaaS para permitir acceso desde esa VNet
3. El tráfico desde la subred se enruta directamente por la red privada de Azure
4. El servicio sigue siendo accesible mediante su IP pública
5. Azure optimiza la ruta internamente sin salir al Internet público
6. El firewall del servicio valida que el tráfico proviene de la VNet autorizada

## Casos de Uso

- Optimizar tráfico desde VNets a Azure Storage sin salir a Internet
- Mejorar seguridad restringiendo acceso a Azure SQL Database desde subredes específicas
- Reducir costos de ancho de banda usando la red privada de Azure
- Simplificar configuración de firewall permitiendo rangos de IP de VNets
- Mejorar rendimiento enrutando tráfico por la red troncal de Microsoft

## Preguntas

1. ¿Un Endpoint de Servicio permite que el tráfico desde una subred viaje por la red privada de Azure hacia un servicio PaaS?

2. ¿Un Endpoint de Servicio introduce el servicio PaaS dentro de la VNet como lo hace Private Endpoint?

3. ¿El servicio PaaS sigue usando su IP pública cuando se accede mediante un Endpoint de Servicio?

4. ¿Es necesario configurar reglas de firewall en el servicio PaaS para que un Endpoint de Servicio funcione correctamente?

5. ¿Un Endpoint de Servicio optimiza el tráfico pero el servicio sigue siendo accesible desde Internet pública?
