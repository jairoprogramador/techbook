# Network Watcher

## Analogía

Network Watcher es como el técnico de redes especializado de Azure que trabaja en las capas 2 y 3 del modelo OSI. Imagina que tienes un edificio con una red compleja de cables, routers y switches. Cuando algo falla, no puedes simplemente ir a revisar cada cable físicamente. Network Watcher es como tener un técnico experto que tiene herramientas especiales: puede hacer "pings" avanzados para ver dónde se corta la conexión, puede verificar si un guardia de seguridad (NSG) está bloqueando el tráfico, puede grabar todo el tráfico que pasa por una máquina virtual sin tener que entrar físicamente, y puede mostrarte un mapa completo de cómo está conectada toda tu red. Es tu herramienta de diagnóstico cuando algo no funciona en la red y necesitas saber exactamente qué está pasando.

## Definición

Azure Network Watcher es un servicio de diagnóstico y monitoreo de red que se enfoca en las capas 2 y 3 del modelo OSI (capa de enlace de datos y capa de red) para diagnosticar problemas de conectividad y rendimiento en recursos de red de Azure.

Permite:

- Diagnosticar problemas de conectividad entre máquinas virtuales y endpoints
- Verificar si los Network Security Groups (NSG) están bloqueando el tráfico
- Capturar y analizar tráfico de red en tiempo real desde máquinas virtuales
- Visualizar la topología completa de la infraestructura de red
- Monitorear continuamente la latencia y pérdida de paquetes entre puntos de conexión
- Identificar dónde y por qué se interrumpe una conexión

## Componentes

**Connection Monitor** – Herramienta de monitoreo avanzada que mide latencia y pérdida de paquetes entre VMs y endpoints, identificando dónde se interrumpe la conexión si cae

**IP Flow Verify** – Diagnostica si un NSG está bloqueando el tráfico entrante o saliente para una dirección IP, puerto y protocolo específicos

**Packet Capture** – Graba el tráfico de red real que pasa por una máquina virtual sin necesidad de acceder físicamente a ella

**Topology** – Visualización interactiva de toda la infraestructura de red mostrando recursos y sus relaciones en Azure

**Next Hop** – Determina el próximo salto de enrutamiento para un paquete desde una VM hacia un destino específico

**NSG Flow Logs** – Registra información sobre el tráfico IP que fluye a través de un NSG para análisis de patrones

**VPN Troubleshoot** – Diagnostica problemas de conectividad en puertas de enlace VPN

## Funcionalidad

1. Network Watcher se habilita automáticamente en cada región de Azure cuando se crea la primera VNet
2. Connection Monitor configura pruebas continuas entre puntos de conexión (VM a VM, VM a endpoint)
3. Las pruebas miden latencia, pérdida de paquetes y disponibilidad en intervalos regulares
4. Si una conexión falla, Connection Monitor identifica en qué punto de la ruta se interrumpió
5. IP Flow Verify simula el tráfico y evalúa las reglas del NSG para determinar si permitiría o bloquearía el tráfico
6. Packet Capture se inicia remotamente en una VM y graba el tráfico de red en un archivo para análisis posterior
7. Topology consulta la configuración de red y genera una vista visual de todos los recursos y sus conexiones

## Casos de Uso

- Diagnosticar por qué una VM no puede conectarse a otra VM o a un endpoint externo
- Verificar si un NSG está bloqueando incorrectamente el tráfico legítimo
- Analizar tráfico de red para investigar problemas de rendimiento o seguridad
- Visualizar la arquitectura de red completa para documentación y troubleshooting
- Monitorear continuamente la conectividad entre recursos críticos
- Identificar dónde se interrumpe una conexión en una ruta compleja
- Capturar paquetes de red para análisis forense o debugging avanzado

## Errores Comunes

- Pensar que Network Watcher requiere instalación manual (se habilita automáticamente)
- Confundir Connection Monitor con un simple ping (es monitoreo continuo y avanzado)
- Creer que Packet Capture requiere acceso a la VM (se ejecuta remotamente)
- Asumir que Network Watcher funciona en todas las capas del modelo OSI (solo capas 2 y 3)
- Pensar que IP Flow Verify modifica reglas del NSG (solo las verifica, no las cambia)

## Preguntas

1. ¿Network Watcher se enfoca exclusivamente en las capas 2 y 3 del modelo OSI para diagnosticar problemas de red?

2. ¿Connection Monitor mide latencia y pérdida de paquetes entre VMs y endpoints, identificando dónde se interrumpe la conexión?

3. ¿IP Flow Verify diagnostica si un NSG está bloqueando el tráfico para una dirección IP, puerto y protocolo específicos?

4. ¿Packet Capture graba el tráfico de red real que pasa por una VM sin necesidad de acceder físicamente a ella?

5. ¿Network Watcher se habilita automáticamente en cada región cuando se crea la primera VNet?

6. ¿Topology proporciona una visualización interactiva de toda la infraestructura de red mostrando recursos y sus relaciones?
