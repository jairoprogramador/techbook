# Azure Service Health

## Analogía

Azure Service Health es como tener un sistema de alertas personalizado que te avisa exactamente qué está pasando con los servicios de Azure que tú usas. Imagina que vives en un edificio con muchos servicios: agua, electricidad, Internet, ascensores. En lugar de enterarte de problemas cuando algo falla, tienes un sistema que te avisa: "Mañana habrá mantenimiento en el ascensor de 2pm a 4pm" o "Hay un problema con el agua en tu piso específico". Azure Service Health funciona igual: te muestra tres niveles de información. Primero, Azure Status te dice el estado general de todos los servicios en todas las regiones (como el estado general del edificio). Segundo, Service Health te dice qué está pasando específicamente con los servicios que tú usas (como problemas en tu piso). Tercero, Resource Health te dice el estado de tus recursos específicos (como tu apartamento individual). Todo esto con alertas personalizadas que te llegan por email, SMS o webhooks.

## Definición

Azure Service Health es un conjunto de experiencias que proporciona información personalizada sobre el estado de salud de los servicios de Azure, incluyendo interrupciones actuales, mantenimiento planificado y otros cambios que afectan la disponibilidad de tus recursos.

Permite:

- Monitorear el estado de salud de servicios de Azure a nivel global, personalizado y de recursos individuales.
- Recibir alertas personalizadas sobre interrupciones de servicio, mantenimiento planificado y avisos de salud.
- Ver información específica sobre cómo los eventos afectan tus recursos y suscripciones.
- Configurar notificaciones mediante email, SMS, webhooks o herramientas de gestión de servicios.
- Acceder a información histórica sobre eventos de salud y mantenimiento.
- Recibir comunicaciones proactivas sobre cambios que afectan la disponibilidad.
- Identificar qué recursos específicos están afectados por incidentes o mantenimiento.

## Componentes

**Azure Status** – Vista global del estado de salud de todos los servicios de Azure en todas las regiones (página pública).

**Service Health** – Vista personalizada del estado de salud de servicios y regiones que usas en tus suscripciones.

**Resource Health** – Información sobre el estado de salud de recursos individuales específicos (VMs, bases de datos, etc.).

**Service Health Alerts** – Alertas configurables mediante Azure Monitor que notifican sobre cambios en la disponibilidad.

**Activity Log** – Registro donde se guardan las notificaciones de Service Health generadas por el sistema.

**Notification Channels** – Canales de notificación: email, SMS, push notifications, webhooks, herramientas ITSM.

**Planned Maintenance** – Eventos de mantenimiento planificados que se comunican con anticipación.

**Service Outages** – Interrupciones no planificadas de servicios que se comunican cuando ocurren.

**Health Advisories** – Avisos sobre problemas que pueden afectar servicios pero no causan interrupciones inmediatas.

## Funcionalidad

1. Azure Status proporciona una vista pública del estado general de todos los servicios de Azure en todas las regiones.
2. Service Health filtra la información para mostrar solo servicios y regiones que usas en tus suscripciones.
3. Resource Health muestra el estado específico de recursos individuales como VMs, bases de datos o cuentas de almacenamiento.
4. Se configuran alertas de Service Health mediante Azure Monitor especificando servicios, regiones y tipos de eventos.
5. Cuando ocurre un evento (interrupción, mantenimiento, aviso), se genera una notificación en el Activity Log.
6. Las alertas configuradas se disparan y envían notificaciones por los canales configurados (email, SMS, webhooks).
7. Service Health proporciona detalles sobre qué recursos están afectados y el impacto esperado.
8. Se puede acceder al historial de eventos para ver información sobre incidentes pasados.
9. Las notificaciones incluyen información sobre resolución, actualizaciones y acciones recomendadas.

## Casos de Uso

- Recibir alertas proactivas sobre mantenimiento planificado que afecta tus recursos.
- Monitorear el estado de salud de servicios críticos para tu organización.
- Identificar qué recursos específicos están afectados por interrupciones de servicio.
- Planificar cambios y mantenimiento basándose en avisos de Service Health.
- Integrar alertas con herramientas ITSM como ServiceNow para gestión de incidentes.
- Recibir notificaciones por múltiples canales (email, SMS) para asegurar que no se pierdan alertas críticas.
- Revisar historial de eventos para análisis de disponibilidad y cumplimiento.
- Configurar alertas específicas para servicios y regiones críticos para tu negocio.

## Errores Comunes

- Confundir Azure Status con Service Health (Status es público y global, Service Health es personalizado).
- Pensar que Service Health requiere configuración adicional para ver información básica (está disponible por defecto).
- Creer que las alertas se configuran automáticamente (requieren configuración manual mediante Azure Monitor).
- Asumir que Resource Health muestra el estado de todos los recursos automáticamente (muestra recursos específicos cuando se consultan).
- Confundir Service Health con Azure Monitor (Service Health es sobre salud de servicios, Monitor es sobre métricas y logs).
- Pensar que todas las notificaciones son críticas (hay notificaciones informativas y otras que requieren acción).
- Creer que Service Health solo muestra problemas actuales (también muestra mantenimiento planificado y avisos).
- Asumir que Service Health tiene costo adicional (está disponible sin costo adicional para todos los suscriptores de Azure).

## Preguntas

1. ¿Azure Service Health proporciona información personalizada sobre el estado de salud de servicios de Azure que usas?.

2. ¿Azure Status es la vista global pública del estado de todos los servicios de Azure en todas las regiones?.

3. ¿Service Health es la vista personalizada que muestra solo servicios y regiones que usas en tus suscripciones?.

4. ¿Resource Health proporciona información sobre el estado de salud de recursos individuales específicos como VMs?.

5. ¿Las alertas de Service Health se configuran mediante Azure Monitor y pueden enviarse por email, SMS o webhooks?.

6. ¿Service Health notifica sobre interrupciones de servicio no planificadas, mantenimiento planificado y avisos de salud?.

7. ¿Las notificaciones de Service Health se registran en el Activity Log de la suscripción?.

8. ¿Service Health está disponible sin costo adicional para todos los suscriptores de Azure?.
