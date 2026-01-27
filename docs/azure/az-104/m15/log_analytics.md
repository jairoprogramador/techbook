# Log Analytics

## Analogía

Log Analytics es como el motor de búsqueda y el archivo de tu infraestructura dentro de Azure Monitor. Imagina que Azure Monitor es una biblioteca enorme con información de todo tu sistema. Log Analytics es específicamente la sección de archivos históricos y el sistema de búsqueda avanzado. Cuando necesitas saber quién borró una VM hace tres semanas, o encontrar todos los errores 404 de la última semana, vas a Log Analytics. Es como tener un Google especializado solo para tu infraestructura: puedes buscar cualquier evento, error o actividad usando un lenguaje de consulta poderoso. Los datos se almacenan en un área de trabajo (workspace) y tú los consultas cuando los necesitas, sin importar cuánta información haya acumulada.

## Definición

Log Analytics es un servicio dentro de Azure Monitor que proporciona almacenamiento y análisis de registros mediante un área de trabajo (workspace) y un motor de consulta que usa KQL (Kusto Query Language).

Permite:

- Almacenar registros de eventos y actividades en un Log Analytics Workspace
- Consultar y analizar grandes volúmenes de datos usando KQL
- Buscar eventos específicos como quién eliminó un recurso o errores de aplicación
- Analizar tendencias y patrones en los datos históricos
- Integrar registros de múltiples fuentes en un solo lugar
- Generar insights a partir de consultas personalizadas

## Componentes

**Log Analytics Workspace** – Área de trabajo que almacena los registros recolectados de múltiples recursos

**KQL (Kusto Query Language)** – Lenguaje de consulta especializado para buscar y analizar grandes volúmenes de datos

**Motor de Consulta** – Sistema que procesa consultas KQL y devuelve resultados de los registros almacenados

**Tablas de Registros** – Estructuras organizadas que almacenan diferentes tipos de eventos y datos

**Consultas Guardadas** – Consultas KQL guardadas para reutilización y automatización

**Integraciones** – Conexiones con recursos de Azure y fuentes externas para recolectar registros

## Funcionalidad

1. Se crea un Log Analytics Workspace que actúa como almacén centralizado de registros
2. Los recursos de Azure envían sus registros al workspace automáticamente o mediante configuración
3. Los registros se almacenan en tablas organizadas por tipo de evento o recurso
4. Se escriben consultas KQL para buscar información específica en los registros almacenados
5. El motor de consulta procesa las consultas y devuelve resultados filtrados
6. Los resultados se pueden visualizar, exportar o usar para generar alertas
7. Las consultas pueden buscar eventos históricos, errores, actividades de usuarios o patrones de comportamiento

## Casos de Uso

- Investigar quién eliminó un recurso consultando registros de actividad de Azure
- Analizar errores 404 u otros códigos de estado HTTP en aplicaciones web
- Buscar eventos de seguridad o accesos no autorizados en los registros
- Identificar patrones de rendimiento o problemas recurrentes en aplicaciones
- Generar reportes personalizados consultando datos históricos específicos
- Monitorear actividades de usuarios y cambios en la configuración de recursos
- Correlacionar eventos de múltiples recursos para análisis de incidentes

## Preguntas

1. ¿Log Analytics es un servicio dentro de Azure Monitor que almacena registros en un workspace?

2. ¿Log Analytics usa KQL (Kusto Query Language) para consultar y analizar grandes volúmenes de datos?

3. ¿Se puede usar Log Analytics para investigar quién eliminó un recurso consultando registros históricos?

4. ¿El Log Analytics Workspace es el almacén de datos donde se guardan los registros de los recursos de Azure?

5. ¿Log Analytics permite buscar eventos específicos como errores 404 o actividades de usuarios mediante consultas KQL?
