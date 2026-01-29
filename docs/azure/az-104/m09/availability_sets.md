# Availability Sets

## Analogía

Availability Sets es como tener múltiples copias de tu servidor en diferentes habitaciones del mismo edificio, pero con reglas inteligentes de distribución. Imagina que tienes un servidor crítico y quieres asegurarte de que siempre esté disponible. En lugar de tenerlo solo en una habitación, lo duplicas y pones cada copia en habitaciones diferentes del mismo edificio. Pero no solo eso: también aseguras que cuando haya mantenimiento en una habitación, las otras sigan funcionando. Availability Sets funciona igual: distribuye tus VMs en diferentes "dominios" (habitaciones lógicas) dentro del mismo centro de datos. Si un servidor físico falla o necesita mantenimiento, tus otras VMs siguen funcionando. Es como tener redundancia dentro del mismo edificio, garantizando que siempre tengas al menos una VM disponible.

## Definición

Availability Sets son agrupaciones lógicas de máquinas virtuales que distribuyen las VMs en dominios de fallo y dominios de actualización para reducir el riesgo de fallos simultáneos y garantizar alta disponibilidad.

Permite:

- Distribuir VMs en hasta 3 dominios de fallo (racks físicos diferentes)
- Distribuir VMs en hasta 20 dominios de actualización (grupos de mantenimiento)
- Garantizar que al menos una VM esté disponible si falla un dominio de fallo
- Evitar que todas las VMs se reinicien simultáneamente durante actualizaciones
- Cumplir con el SLA de 99.95% cuando hay 2 o más VMs en el Availability Set
- Reducir latencia entre VMs comparado con Availability Zones
- Proteger contra fallos de hardware dentro del mismo centro de datos

## Componentes

**Fault Domain** – Grupo de servidores físicos que comparten fuente de alimentación y switch de red (hasta 3 por Availability Set)

**Update Domain** – Grupo de VMs que se reinician juntas durante mantenimiento (hasta 20 por Availability Set)

**Availability Set** – Recurso lógico que agrupa VMs y define su distribución en dominios

**SLA 99.95%** – Acuerdo de nivel de servicio garantizado cuando hay 2 o más VMs en un Availability Set

**Rack** – Estructura física que contiene múltiples servidores físicos

**Distribución Automática** – Azure distribuye automáticamente las VMs en los dominios disponibles

## Funcionalidad

1. Se crea un Availability Set que define la agrupación lógica de VMs
2. Se configuran las VMs para pertenecer al Availability Set durante la creación
3. Azure distribuye automáticamente las VMs en los dominios de fallo disponibles (hasta 3)
4. Azure distribuye las VMs en los dominios de actualización disponibles (hasta 20)
5. Si un servidor físico falla (fault domain), solo las VMs en ese dominio se ven afectadas
6. Durante actualizaciones de Azure, solo un update domain se reinicia a la vez
7. Las VMs en otros dominios continúan operando normalmente durante fallos o actualizaciones
8. El Availability Set garantiza que siempre haya VMs disponibles si hay 2 o más VMs configuradas
9. Azure cumple con el SLA de 99.95% cuando hay múltiples VMs distribuidas en el Availability Set

## Casos de Uso

- Garantizar alta disponibilidad para aplicaciones críticas distribuyendo VMs en múltiples racks físicos
- Proteger contra fallos de hardware dentro del mismo centro de datos
- Evitar downtime durante actualizaciones de Azure distribuyendo VMs en múltiples update domains
- Cumplir con requisitos de SLA de 99.95% para aplicaciones empresariales
- Reducir latencia entre VMs comparado con Availability Zones (mismo centro de datos)
- Implementar alta disponibilidad en regiones que no soportan Availability Zones
- Distribuir VMs de forma que un fallo físico no afecte todas las instancias
- Configurar aplicaciones de múltiples niveles con VMs distribuidas en diferentes dominios

## Errores Comunes

- Pensar que Availability Sets distribuyen VMs en diferentes regiones (solo distribuyen en el mismo centro de datos)
- Confundir Fault Domains con Update Domains (Fault Domains son racks físicos, Update Domains son grupos de mantenimiento)
- Creer que se puede agregar una VM a un Availability Set después de crearla (debe estar en el Availability Set desde la creación)
- Asumir que Availability Sets protegen contra desastres regionales (solo protegen contra fallos dentro del centro de datos)
- Pensar que Availability Sets y Availability Zones son lo mismo (Zones son zonas físicas separadas, Sets son dominios lógicos)
- Creer que una sola VM en un Availability Set cumple el SLA (se requieren 2 o más VMs)
- Confundir Availability Sets con Load Balancers (Availability Sets distribuyen físicamente, Load Balancers distribuyen tráfico)
- Asumir que se puede cambiar el número de fault domains después de crear el Availability Set (se define al crear)

## Preguntas

1. ¿Availability Sets distribuyen VMs en hasta 3 dominios de fallo (racks físicos diferentes) dentro del mismo centro de datos?

2. ¿Availability Sets distribuyen VMs en hasta 20 dominios de actualización para evitar reinicios simultáneos?

3. ¿Azure garantiza un SLA de 99.95% cuando hay 2 o más VMs en un Availability Set?

4. ¿Las VMs deben estar en el Availability Set desde su creación, no se pueden agregar después?

5. ¿Availability Sets protegen contra fallos de hardware dentro del mismo centro de datos pero no contra desastres regionales?

6. ¿Durante actualizaciones de Azure, solo un update domain se reinicia a la vez, manteniendo otras VMs disponibles?

7. ¿Availability Sets tienen menor latencia entre VMs comparado con Availability Zones porque están en el mismo centro de datos?

8. ¿Si un fault domain falla, solo las VMs en ese dominio se ven afectadas, mientras otras continúan operando?
