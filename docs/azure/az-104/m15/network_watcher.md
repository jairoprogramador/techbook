# Network Watcher

## Analogía

Network Watcher es como el técnico de redes especializado de Azure que trabaja en las capas 2 y 3 del modelo OSI. Cuando algo falla en la red, no puedes revisar cada cable físicamente: Network Watcher es el servicio que agrupa las herramientas para diagnosticar conectividad, comprobar si un NSG bloquea tráfico, ver el próximo salto de una ruta, grabar tráfico de una VM o visualizar la topología. El servicio se habilita automáticamente en cada región cuando creas la primera VNet.

## Definición

Azure Network Watcher es un servicio de diagnóstico y monitoreo de red que se enfoca en las capas 2 y 3 del modelo OSI (capa de enlace de datos y capa de red) para diagnosticar problemas de conectividad y rendimiento en recursos de red de Azure.

Permite:

- Agrupar en un mismo servicio las herramientas de diagnóstico de red (Connection Monitor, IP Flow Verify, Next hop, NSG Flow Logs, Packet Capture, Topology, VPN Troubleshoot)
- Habilitarse automáticamente en cada región cuando se crea la primera VNet en esa región
- Ofrecer diagnóstico sin necesidad de desplegar agentes adicionales en la mayoría de los casos (salvo Packet Capture, que requiere Network Watcher Agent en la VM)
- Operar por región: cada región tiene su instancia de Network Watcher para los recursos de esa región

Para el detalle de cada herramienta (qué hace, cómo se usa, componentes y preguntas), ver **Herramientas de diagnóstico de red** en el módulo Redes.

## Herramientas (resumen)

Las capacidades que proporciona Network Watcher se describen en detalle en el documento **Herramientas de diagnóstico de red**.

- **Connection Monitor** – Monitoreo continuo de latencia y pérdida de paquetes entre puntos de conexión
- **IP Flow Verify** – Comprueba si un NSG permitiría o bloquearía un flujo concreto
- **Next hop** – Indica el próximo salto de enrutamiento desde una VM hacia un destino
- **NSG Flow Logs** – Registro del tráfico que pasa por un NSG
- **Packet Capture** – Captura remota del tráfico de red de una VM
- **Topology** – Visualización de la infraestructura de red y sus relaciones
- **VPN Troubleshoot** – Diagnóstico de problemas en puertas de enlace VPN

## Funcionalidad

1. Network Watcher se habilita automáticamente en cada región de Azure cuando se crea la primera VNet (o se habilita manualmente desde el portal)
2. Una vez habilitado, las herramientas del servicio están disponibles para los recursos de red de esa región
3. Cada herramienta se usa desde la hoja de Network Watcher en el portal (o por API/CLI) según el tipo de diagnóstico que se necesite
4. Para el flujo de uso concreto de cada herramienta, ver **Herramientas de diagnóstico de red** (m14)

## Casos de Uso

- Usar Network Watcher cuando hay que diagnosticar problemas de conectividad, enrutamiento o tráfico en recursos de red de Azure
- Consultar el documento **Herramientas de diagnóstico de red** para elegir la herramienta adecuada y su uso detallado

## Errores Comunes

- Pensar que Network Watcher requiere instalación o habilitación manual en cada suscripción (se habilita automáticamente por región al crear la primera VNet)
- Asumir que Network Watcher cubre todas las capas del modelo OSI (se enfoca en capas 2 y 3)

## Preguntas

1. ¿Network Watcher es un servicio de Azure que se enfoca en las capas 2 y 3 del modelo OSI para diagnóstico de red?

2. ¿Network Watcher se habilita automáticamente en cada región cuando se crea la primera VNet en esa región?

3. ¿Las herramientas de diagnóstico (Connection Monitor, IP Flow Verify, Next hop, NSG Flow Logs, Packet Capture, Topology, VPN Troubleshoot) forman parte del servicio Network Watcher?

4. ¿Network Watcher opera por región: los recursos de una región usan la instancia de Network Watcher de esa región?

5. ¿Para el detalle de uso y componentes de cada herramienta de red hay que consultar el documento Herramientas de diagnóstico de red (módulo Redes Virtuales)?
