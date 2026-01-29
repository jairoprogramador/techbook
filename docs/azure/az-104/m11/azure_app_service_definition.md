# Azure App Service

## Analogía

Azure App Service es como un hotel de lujo para aplicaciones web donde no tienes que preocuparte por la infraestructura. Imagina que quieres abrir un restaurante, pero en lugar de construir el edificio, comprar las mesas, contratar personal de mantenimiento y preocuparte por la electricidad y el agua, simplemente alquilas un espacio completamente equipado. Solo traes tu comida (tu código) y el hotel se encarga de todo lo demás: escalar automáticamente cuando llegan más clientes, mantener las instalaciones, seguridad, certificados SSL, y hasta te permite tener una cocina de prueba (staging) donde puedes probar nuevas recetas antes de servirlas a los clientes. Puedes hospedar aplicaciones web, APIs, backends móviles, y todo funciona sin que tengas que administrar servidores.

## Definición

Azure App Service es una plataforma como servicio (PaaS) de Azure que permite hospedar y escalar aplicaciones web, APIs REST, backends móviles y aplicaciones sin servidor sin necesidad de administrar la infraestructura subyacente.

Permite:

- Hospedar aplicaciones web, APIs y backends móviles en Windows o Linux
- Escalar automáticamente según la demanda sin intervención manual
- Desplegar código desde múltiples fuentes (GitHub, Azure DevOps, Git local)
- Crear entornos de staging separados de producción mediante deployment slots
- Integrar autenticación y autorización con Azure Active Directory y proveedores sociales
- Configurar dominios personalizados con certificados SSL/TLS gestionados
- Conectar con bases de datos y otros servicios de Azure mediante integraciones

## Componentes

**App Service Plan** – Plan de hospedaje que define la región, capacidad de cómputo, características y costo de las aplicaciones

**Web App** – Aplicación web hospedada en App Service que puede ejecutar código en múltiples lenguajes y frameworks

**Deployment Slots** – Entornos separados (staging, producción) que permiten probar cambios antes de intercambiarlos con producción sin downtime

**Auto Scaling** – Escalado automático basado en métricas (CPU, memoria, tráfico HTTP) o horarios predefinidos

**Custom Domains** – Dominios personalizados configurados para la aplicación con certificados SSL/TLS gestionados

**Authentication/Authorization** – Integración con Azure AD y proveedores sociales (Google, Facebook, Twitter) para autenticación sin código

**Application Settings** – Variables de configuración y cadenas de conexión que se pueden cambiar sin redeployar

**Deployment Center** – Integración con repositorios Git y pipelines CI/CD para despliegues automatizados

**Backup and Restore** – Copias de seguridad programadas de la aplicación y base de datos asociada

## Funcionalidad

1. Se crea un App Service Plan que define la capacidad y características de cómputo disponibles
2. Se crea una Web App dentro del plan que hospeda la aplicación (código, contenedor o función)
3. El código se despliega desde un repositorio Git, contenedor Docker, o archivo ZIP mediante Deployment Center
4. Se configuran deployment slots para crear entornos de staging separados de producción
5. Los cambios se despliegan primero en staging para pruebas antes de hacer swap con producción
6. Auto Scaling monitorea métricas (CPU, memoria, tráfico) y escala automáticamente según reglas configuradas
7. Se configuran dominios personalizados y certificados SSL/TLS para acceso seguro
8. Authentication/Authorization se integra para autenticar usuarios sin escribir código de autenticación
9. Las aplicaciones se ejecutan en infraestructura gestionada por Azure sin necesidad de administrar servidores

## Casos de Uso

- Hospedar aplicaciones web ASP.NET, ASP.NET Core, Node.js, Python, Java y PHP
- Desplegar APIs REST para aplicaciones móviles o frontends
- Crear backends para aplicaciones móviles con autenticación integrada
- Hospedar aplicaciones en contenedores Docker (Windows o Linux)
- Implementar sitios web estáticos con Jekyll, Hugo o frameworks similares
- Desplegar aplicaciones con CI/CD desde GitHub, Azure DevOps o Git local
- Escalar aplicaciones automáticamente durante picos de tráfico
- Probar cambios en staging antes de moverlos a producción sin downtime
- Conectar aplicaciones con bases de datos de Azure y otros servicios PaaS

## Errores Comunes

- Pensar que App Service requiere administración de servidores (es PaaS, completamente gestionado)
- Confundir App Service Plan con Web App (el plan es la infraestructura, la app es la aplicación)
- Asumir que deployment slots están disponibles en todos los planes (solo Standard, Premium e Isolated)
- Creer que Auto Scaling funciona igual en todos los planes (hay diferencias entre planes)
- Pensar que se puede escalar una Web App individualmente (el escalado aplica al App Service Plan completo)
- Asumir que todas las aplicaciones en el mismo plan comparten recursos (comparten la misma infraestructura)
- Confundir App Service con Azure Functions (App Service es para aplicaciones completas, Functions es serverless)

## Preguntas

1. ¿Azure App Service es una plataforma PaaS que permite hospedar aplicaciones web sin administrar infraestructura?

2. ¿Los deployment slots permiten crear entornos de staging separados de producción para probar cambios antes de intercambiarlos?

3. ¿Auto Scaling en App Service escala automáticamente según métricas como CPU, memoria y tráfico HTTP?

4. ¿El escalado en App Service se aplica al App Service Plan completo, no a Web Apps individuales?

5. ¿App Service permite integrar autenticación con Azure AD y proveedores sociales sin escribir código de autenticación?

6. ¿Deployment slots están disponibles solo en los planes Standard, Premium e Isolated?

7. ¿App Service soporta despliegues desde repositorios Git, contenedores Docker y archivos ZIP mediante Deployment Center?
