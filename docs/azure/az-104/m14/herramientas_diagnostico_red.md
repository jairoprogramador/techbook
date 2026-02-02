# Herramientas de diagnóstico de red (Azure)

Las herramientas de diagnóstico de red en Azure son como el kit del técnico cuando algo falla en la red: “¿por qué esta VM no llega a Internet?”, “¿quién está bloqueando el tráfico?”, “¿por qué ruta va este paquete?”. Connection Monitor mide latencia y pérdida entre puntos; IP Flow Verify comprueba si un NSG bloquea un flujo concreto; Next hop te dice el próximo salto de una ruta; NSG Flow Logs registran el tráfico que pasa por un NSG; Packet Capture graba el tráfico de una VM; Topology muestra la infraestructura de red; VPN Troubleshoot diagnostica puertas de enlace VPN. Todas las proporciona el servicio **Network Watcher** (definición del servicio en el módulo de Monitorización).

## Definición

Las herramientas de diagnóstico de red en Azure son capacidades del servicio **Network Watcher** que permiten diagnosticar problemas de conectividad, enrutamiento y tráfico en redes virtuales y recursos de Azure: Connection Monitor, IP Flow Verify, Next hop, NSG Flow Logs, Packet Capture, Topology y VPN Troubleshoot. Este documento es la fuente única para el detalle de cada herramienta.

Permite:

- Medir latencia, pérdida de paquetes y disponibilidad entre puntos (VM, endpoint) de forma continua (Connection Monitor)
- Verificar si un NSG está bloqueando un flujo concreto (IP, puerto, protocolo) con IP Flow Verify
- Determinar el próximo salto de enrutamiento desde una VM hacia un destino (Next hop)
- Registrar el tráfico que pasa por un NSG para análisis (NSG Flow Logs)
- Capturar paquetes de red desde una VM de forma remota (Packet Capture)
- Visualizar la topología de la infraestructura de red (Topology)
- Diagnosticar problemas de conectividad en puertas de enlace VPN (VPN Troubleshoot)

## Componentes

**Connection Monitor** – Herramienta de Network Watcher que mide latencia y pérdida de paquetes entre puntos de conexión (VM a VM, VM a endpoint); si la conexión falla, ayuda a identificar en qué punto se interrumpe

**IP Flow Verify** – Herramienta de Network Watcher que simula un flujo (IP origen/destino, puerto, protocolo) y evalúa las reglas del NSG para indicar si el tráfico sería permitido o denegado; útil para comprobar si un NSG bloquea tráfico legítimo

**Next hop** – Herramienta de Network Watcher que indica el próximo salto de enrutamiento para un paquete desde una VM hacia una IP destino; ayuda a ver si el tráfico va por la ruta esperada (p. ej. Virtual Appliance, VNet Gateway, Internet)

**NSG Flow Logs** – Registro del tráfico IP que pasa por un NSG (permitido o denegado); se puede enviar a una cuenta de almacenamiento o a Log Analytics para análisis; útil para auditoría y troubleshooting

**Packet Capture** – Captura remota del tráfico de red de una VM; se inicia desde Network Watcher y graba paquetes en un archivo (local en la VM o en almacenamiento); la VM debe tener la extensión Network Watcher Agent; útil para análisis forense o debugging avanzado

**Topology** – Herramienta de Network Watcher que genera una vista visual de la infraestructura de red (recursos, subredes, NSG, sus relaciones); consulta la configuración de red y la representa de forma interactiva; útil para documentación y troubleshooting de la arquitectura

**VPN Troubleshoot** – Diagnóstico de problemas de conectividad en VPN Gateways (P2S, S2S, VNet-to-VNet); genera logs y estado de la conexión

**Network Watcher** – Servicio de Azure que agrupa estas herramientas; se habilita por región cuando se crea la primera VNet en esa región (ver documento Network Watcher en el módulo de Monitorización para la definición del servicio)

## Funcionalidad

1. Network Watcher se habilita automáticamente en cada región al crear la primera VNet (o se habilita manualmente)
2. **Connection Monitor**: se configura un monitor con origen (VM) y destino (VM o IP); se ejecutan pruebas periódicas; se revisan resultados de latencia, pérdida y estado
3. **IP Flow Verify**: se elige una VM, IP destino, puerto y protocolo; Network Watcher evalúa las reglas del NSG aplicables y devuelve si el tráfico sería permitido o denegado y qué regla aplica
4. **Next hop**: se elige una VM, IP destino y opcionalmente NIC; Network Watcher devuelve el próximo salto (Virtual Appliance, VNet Gateway, Internet, None, etc.)
5. **NSG Flow Logs**: se habilita el flow log en un NSG; se configura destino (Storage o Log Analytics); los registros se generan según el intervalo configurado
6. **Packet Capture**: se inicia una captura desde Network Watcher sobre una VM; se define filtros y destino del archivo; la VM debe tener la extensión de Network Watcher Agent
7. **Topology**: se consulta desde Network Watcher; genera una vista visual de la infraestructura de red (recursos, subredes, NSG, relaciones) según la configuración actual
8. **VPN Troubleshoot**: se ejecuta el diagnóstico sobre el VPN Gateway o la conexión; se descargan logs para análisis

## Casos de Uso

- Comprobar si un NSG está bloqueando tráfico legítimo usando IP Flow Verify antes de cambiar reglas
- Ver por qué ruta sale el tráfico desde una VM (Next hop) cuando se usan UDR o NVA
- Monitorear conectividad continua entre recursos críticos con Connection Monitor
- Analizar patrones de tráfico o investigar incidentes con NSG Flow Logs
- Capturar paquetes para debugging o análisis forense con Packet Capture
- Diagnosticar fallos de VPN (S2S, P2S) con VPN Troubleshoot
- Visualizar la arquitectura de red completa para documentación o troubleshooting con Topology
- Ver documento **Network Watcher** (módulo Monitorización) para la definición del servicio

## Errores Comunes

- Confundir IP Flow Verify con NSG Flow Logs (IP Flow Verify es una prueba puntual “¿este flujo estaría permitido?”; NSG Flow Logs es un registro continuo del tráfico)
- Pensar que Next hop requiere que el tráfico esté activo (Next hop consulta la tabla de rutas y devuelve el próximo salto según la configuración; no necesita tráfico en tiempo real)
- Creer que Packet Capture no requiere agente en la VM (la VM necesita la extensión Network Watcher Agent para capturas remotas)
- Olvidar que Network Watcher se habilita por región (si la VNet está en otra región, hay que usar Network Watcher de esa región)
- Usar solo Connection Monitor sin revisar NSG o UDR cuando hay fallos (combinar IP Flow Verify y Next hop para diagnóstico completo)

## Preguntas

1. ¿Connection Monitor mide latencia y pérdida de paquetes entre puntos de conexión y ayuda a identificar dónde se interrumpe la conexión?

2. ¿IP Flow Verify indica si un NSG permitiría o denegaría un flujo concreto (IP, puerto, protocolo) sin enviar tráfico real?

3. ¿Next hop devuelve el próximo salto de enrutamiento desde una VM hacia una IP destino (p. ej. Virtual Appliance, VNet Gateway, Internet)?

4. ¿NSG Flow Logs registran el tráfico que pasa por un NSG y se pueden enviar a Storage o Log Analytics?

5. ¿Packet Capture graba el tráfico de red de una VM de forma remota y requiere la extensión Network Watcher Agent en la VM?

6. ¿Topology genera una vista visual de la infraestructura de red (recursos, subredes, NSG, relaciones) según la configuración actual?

7. ¿Estas herramientas forman parte del servicio Network Watcher que se habilita por región?
