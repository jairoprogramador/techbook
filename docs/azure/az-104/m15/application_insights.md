# Application Insights

## Analogía

Application Insights es como tener un detective dentro de tu aplicación que observa todo lo que pasa. Imagina que tu aplicación es una casa y Application Insights es un sistema de cámaras y sensores que registra cada movimiento: qué habitaciones se usan más, cuánto tiempo tarda alguien en abrir una puerta, si alguna puerta se atasca, y exactamente qué pasó cuando algo falló. No solo te dice que hubo un problema, sino que te muestra el video completo: qué usuario hizo qué acción, qué llamó a la base de datos, cuánto tardó, y si hubo un error, exactamente en qué línea de código ocurrió. Es como tener un registro forense completo de cada interacción con tu aplicación, diseñado específicamente para que los desarrolladores puedan entender y arreglar problemas rápidamente.

## Definición

Application Insights es un servicio de Azure Monitor diseñado específicamente para desarrolladores que proporciona monitoreo de rendimiento de aplicaciones (APM) mediante instrumentación del código y recolección automática de telemetría.

Permite:

- Monitorear el rendimiento y disponibilidad de aplicaciones en tiempo real
- Rastrear dependencias entre componentes (web, base de datos, APIs externas)
- Capturar excepciones y errores con detalles del código fuente
- Identificar cuellos de botella y problemas de rendimiento
- Analizar el comportamiento de usuarios y patrones de uso
- Instrumentar aplicaciones web, microservicios, contenedores y funciones serverless

## Componentes

**Telemetría Automática** – Recolección automática de solicitudes HTTP, dependencias y excepciones sin configuración manual

**Instrumentación Manual** – API para agregar eventos personalizados, métricas y trazas específicas en el código

**Dependencias** – Rastreo automático de llamadas a bases de datos, APIs externas y servicios internos con latencias

**Excepciones** – Captura automática de errores con stack traces y contexto de la solicitud que los causó

**Snapshot Debugger** – Captura instantáneas del código fuente y variables cuando ocurren excepciones en producción

**Mapa de Aplicación** – Visualización automática de la arquitectura de la aplicación mostrando componentes y sus dependencias

**Métricas en Tiempo Real** – Visualización de rendimiento y errores mientras ocurren mediante Live Metrics

**Log Analytics Integration** – Almacenamiento de telemetría en Log Analytics Workspace para consultas KQL

## Funcionalidad

1. Se instrumenta la aplicación agregando el SDK de Application Insights al código o mediante auto-instrumentación
2. La aplicación envía telemetría automáticamente: solicitudes HTTP, dependencias, excepciones y métricas personalizadas
3. Application Insights recolecta y procesa la telemetría en tiempo real
4. Se rastrean dependencias mostrando cómo la aplicación se comunica con bases de datos, APIs externas y servicios
5. Cuando ocurre una excepción, se captura el stack trace y, con Snapshot Debugger, se guarda una instantánea del código y variables
6. Los datos se almacenan en Log Analytics Workspace y se pueden consultar con KQL
7. Se generan visualizaciones automáticas: mapa de aplicación, métricas de rendimiento, análisis de errores y comportamiento de usuarios

## Casos de Uso

- Monitorear aplicaciones web ASP.NET, ASP.NET Core, Node.js, Python y Java en producción
- Diagnosticar problemas de rendimiento identificando cuellos de botella en dependencias externas
- Rastrear microservicios y contenedores en Kubernetes o Docker para entender la comunicación entre servicios
- Analizar errores en producción con detalles del código fuente mediante Snapshot Debugger
- Optimizar consultas a bases de datos identificando las más lentas y problemáticas
- Monitorear Azure Functions y aplicaciones serverless para detectar problemas de escalado
- Correlacionar errores con solicitudes específicas de usuarios para reproducir problemas
- Analizar patrones de uso de usuarios para mejorar la experiencia de la aplicación

## Errores Comunes

- Pensar que Application Insights solo funciona con aplicaciones web (funciona con microservicios, contenedores, funciones y más)
- Confundir Application Insights con Azure Monitor general (Application Insights es específico para aplicaciones)
- Asumir que muestra automáticamente la línea exacta de código sin Snapshot Debugger configurado
- Creer que requiere modificar mucho código (la auto-instrumentación captura la mayoría de datos automáticamente)
- Pensar que solo monitorea aplicaciones en Azure (funciona con aplicaciones on-premises y otras nubes)
- Confundir dependencias con métricas (las dependencias muestran comunicación entre componentes, no solo números)

## Preguntas

1. ¿Application Insights está diseñado específicamente para desarrolladores y proporciona monitoreo de rendimiento de aplicaciones?

2. ¿Application Insights puede rastrear dependencias mostrando cómo la aplicación se comunica con bases de datos y APIs externas?

3. ¿Application Insights funciona solo con aplicaciones web o también con microservicios, contenedores y funciones serverless?

4. ¿Snapshot Debugger captura instantáneas del código fuente y variables cuando ocurren excepciones en producción?

5. ¿Application Insights puede identificar cuellos de botella en dependencias externas y mostrar latencias de comunicación entre componentes?

## Resumen

- Application Insights = monitoreo de aplicaciones para desarrolladores
- Rastrea dependencias: web, base de datos, APIs externas
- Captura excepciones con stack traces y código fuente (Snapshot Debugger)
- Funciona con web, microservicios, contenedores y serverless
- Telemetría automática + instrumentación manual opcional
- Integrado con Log Analytics para consultas KQL
