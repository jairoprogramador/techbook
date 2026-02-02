# Conjuntos de Escalado de Máquinas Virtuales (VM Scale Sets)

 Un conjunto de escalado de máquinas virtuales (VM Scale Set) es como tener un ejército de servidores idénticos que se multiplican o reducen automáticamente según la demanda. Imagina que tienes una aplicación web que a veces necesita 2 servidores y otras veces 20. En lugar de crear y eliminar VMs manualmente, defines un "modelo" (tamaño, imagen, configuración) y Azure crea tantas instancias idénticas como necesites. Si la carga aumenta, se añaden más automáticamente; si baja, se eliminan. Todas las instancias son iguales y el tráfico se distribuye entre ellas. Es como tener un grupo de trabajadores que se ajusta al volumen de trabajo sin que tengas que contratar o despedir manualmente.

## Definición

Un conjunto de escalado de máquinas virtuales (VM Scale Set) es un servicio de Azure que crea y gestiona un grupo de VMs idénticas con escalado automático basado en métricas (CPU, memoria, tráfico de red, etc.); todas las instancias se crean desde el mismo modelo (imagen, tamaño, configuración) y se distribuyen automáticamente en dominios de fallo y actualización para alta disponibilidad.

Permite:

- Crear múltiples instancias de VMs idénticas desde un modelo único (imagen, tamaño, configuración)
- Escalar automáticamente el número de instancias (escalado horizontal) según métricas (CPU, memoria, métricas personalizadas) o según una programación
- Distribuir instancias automáticamente en dominios de fallo y actualización para alta disponibilidad
- Actualizar instancias de forma gradual (rolling update) sin interrumpir el servicio completo
- Integrar con Azure Load Balancer o Application Gateway para distribuir tráfico entre instancias
- Usar health probes para detectar instancias no saludables y reemplazarlas automáticamente

## Componentes

**Modelo de VM (VM Model)** – Configuración base que define la imagen (Windows, Linux, personalizada), tamaño, discos, red y extensiones; todas las instancias se crean idénticas a este modelo

**Instancias** – VMs individuales creadas desde el modelo; el número de instancias puede variar según el escalado automático o manual; cada instancia tiene su propia IP privada

**Escalado automático (Autoscale)** – Reglas que aumentan o disminuyen el número de instancias según métricas (p. ej. CPU > 70% añade instancias, CPU < 30% elimina instancias) o según una programación

**Rolling update (actualización gradual)** – Modo de actualización que actualiza instancias en lotes (batches) para mantener disponibilidad; las instancias nuevas se crean con la nueva configuración mientras las antiguas siguen sirviendo tráfico hasta que todas se actualizan

**Health probe (sonda de salud)** – Verificación de salud de las instancias mediante Azure Load Balancer o Application Gateway; si una instancia no responde correctamente, se marca como no saludable y puede ser reemplazada

**Application Health extension** – Extensión de VM que monitorea la salud de la aplicación en la instancia (TCP, HTTP/HTTPS); se usa con rolling updates y para determinar si una instancia está lista para recibir tráfico

**Overprovisioning** – Opción que crea más instancias de las solicitadas temporalmente y luego elimina las sobrantes para mejorar la probabilidad de éxito en el despliegue; se puede deshabilitar

**Instancias spot** – Opción para usar VMs de bajo costo con prioridad baja (Azure puede recuperarlas con 30 segundos de aviso); útil para cargas de trabajo tolerantes a interrupciones

**Dominios de fallo y actualización** – Distribución automática de instancias en dominios físicos distintos para alta disponibilidad (similar a Availability Sets pero gestionado automáticamente por el Scale Set)

## Funcionalidad

1. Se crea un VM Scale Set definiendo el modelo: imagen (Windows, Linux o personalizada), tamaño de VM, configuración de red, discos y extensiones
2. Se configura el número inicial de instancias y los límites mínimo y máximo para el escalado automático
3. Se configuran reglas de escalado automático basadas en métricas (CPU, memoria, métricas personalizadas) o programación (p. ej. más instancias en horario laboral)
4. Opcionalmente se integra con Azure Load Balancer o Application Gateway para distribuir tráfico entre instancias; se configuran health probes para verificar salud
5. Cuando se necesita actualizar el modelo (p. ej. nueva imagen, nueva configuración), se puede usar rolling update: las instancias se actualizan en lotes, manteniendo disponibilidad
6. Las instancias no saludables (detectadas por health probes o Application Health extension) pueden ser reemplazadas automáticamente por el Scale Set
7. El escalado automático añade o elimina instancias según las reglas configuradas; las nuevas instancias se crean idénticas al modelo
8. Todas las instancias se distribuyen automáticamente en dominios de fallo y actualización para alta disponibilidad

## Casos de Uso

- Aplicaciones web o APIs que necesitan escalar horizontalmente según la carga (más instancias cuando hay más tráfico)
- Cargas de trabajo que requieren múltiples instancias idénticas con alta disponibilidad sin gestionar Availability Sets manualmente
- Aplicaciones que necesitan actualizaciones sin downtime mediante rolling updates
- Entornos que requieren ajuste automático de capacidad según horarios o demanda (p. ej. más instancias en horario laboral)
- Cargas de trabajo tolerantes a interrupciones que pueden usar instancias spot para reducir costos
- Aplicaciones que se benefician de health monitoring y reemplazo automático de instancias no saludables

## Errores Comunes

- Confundir VM Scale Sets con Availability Sets (los Scale Sets crean y gestionan múltiples VMs idénticas con escalado automático; los Availability Sets agrupan VMs existentes para alta disponibilidad)
- Pensar que el escalado automático está siempre habilitado por defecto (hay que configurar reglas de escalado automático; sin ellas, el número de instancias es fijo)
- Creer que todas las instancias deben estar en la misma subred (las instancias pueden estar en múltiples subredes si se configura)
- Asumir que rolling update es el único modo de actualización (también hay modo manual y automático según la configuración)
- Olvidar que los health probes son necesarios para que el Load Balancer o Application Gateway sepan qué instancias están saludables y puedan distribuir tráfico correctamente

## Preguntas

1. ¿Un VM Scale Set crea y gestiona múltiples instancias de VMs idénticas desde un modelo único con escalado automático?

2. ¿El escalado automático en VM Scale Sets aumenta o disminuye el número de instancias según métricas (CPU, memoria) o programación?

3. ¿Rolling update actualiza las instancias del Scale Set en lotes para mantener disponibilidad sin interrumpir el servicio completo?

4. ¿Los health probes (de Load Balancer o Application Gateway) verifican la salud de las instancias y permiten distribuir tráfico solo a instancias saludables?

5. ¿Las instancias de un VM Scale Set se distribuyen automáticamente en dominios de fallo y actualización para alta disponibilidad?

6. ¿VM Scale Sets permite usar instancias spot (bajo costo, prioridad baja) para cargas de trabajo tolerantes a interrupciones?
