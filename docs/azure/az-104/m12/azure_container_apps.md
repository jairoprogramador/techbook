# Azure Container Apps (ACA)

## Analogía

Azure Container Apps es como tener un restaurante completamente automatizado donde los meseros aparecen automáticamente cuando llegan clientes y desaparecen cuando no hay nadie. Imagina que tienes un restaurante que puede tener desde cero meseros hasta cientos, dependiendo de cuántos clientes lleguen. Cuando llega un cliente, automáticamente aparece un mesero. Si llegan muchos clientes, aparecen más meseros. Si no hay clientes, los meseros desaparecen y no pagas por ellos. Azure Container Apps funciona igual: ejecutas microservicios en contenedores que escalan automáticamente desde cero hasta miles de instancias según la demanda. No tienes que gestionar servidores, ni clústeres de Kubernetes, ni configuración compleja. Solo despliegas tu contenedor y Azure se encarga de escalarlo automáticamente según el tráfico, eventos o métricas. Es como tener Kubernetes pero sin tener que aprender Kubernetes.

## Definición

Azure Container Apps es una plataforma serverless completamente gestionada basada en Kubernetes que permite ejecutar microservicios y aplicaciones en contenedores con escalado automático sin necesidad de gestionar la infraestructura de Kubernetes.

Permite:

- Ejecutar microservicios y aplicaciones en contenedores sin gestionar Kubernetes directamente.
- Escalar automáticamente desde cero hasta miles de instancias según demanda, eventos o métricas.
- Escalar a cero cuando no hay tráfico para reducir costos.
- Soportar múltiples protocolos: HTTP, gRPC, WebSockets y TCP.
- Integrar con Dapr para construir aplicaciones distribuidas y resilientes.
- Ejecutar trabajos en segundo plano y aplicaciones event-driven.
- Conectar aplicaciones mediante revisiones y entornos para gestión de versiones.
- Integrar con Azure Container Registry para despliegue de imágenes privadas.

## Componentes

**Container App Environment** – Entorno aislado que contiene múltiples Container Apps y proporciona red y seguridad compartida.

**Container App** – Aplicación que ejecuta uno o más contenedores con configuración de escalado y tráfico.

**Revision** – Versión inmutable de una Container App que representa un despliegue específico.

**Ingress** – Configuración que expone la Container App a Internet o red interna con balanceo de carga.

**Scale Rules** – Reglas que definen cómo escalar la aplicación (HTTP, CPU, memoria, eventos personalizados).

**Dapr Integration** – Integración con Distributed Application Runtime para microservicios y aplicaciones distribuidas.

**Secrets** – Secretos gestionados que se pueden usar como variables de entorno o montajes en contenedores.

**Managed Identity** – Identidad gestionada que permite a Container Apps acceder a otros servicios de Azure sin credenciales.

## Funcionalidad

1. Se crea un Container App Environment que proporciona la infraestructura compartida y red.
2. Se crea una Container App dentro del entorno especificando la imagen de contenedor.
3. Se configuran reglas de escalado basadas en HTTP, CPU, memoria o eventos personalizados.
4. Se configura Ingress para exponer la aplicación a Internet o mantenerla interna.
5. Se despliega la aplicación creando una nueva revisión con la imagen de contenedor.
6. Container Apps escala automáticamente según las reglas configuradas (desde cero hasta miles de instancias).
7. Cuando no hay tráfico, la aplicación escala a cero y no consume recursos.
8. El tráfico se distribuye automáticamente entre las instancias mediante balanceo de carga.
9. Se pueden actualizar aplicaciones mediante nuevas revisiones con despliegue gradual o instantáneo.

## Casos de Uso

- Ejecutar microservicios y APIs REST con escalado automático según demanda.
- Implementar aplicaciones event-driven que responden a eventos de Azure Services.
- Ejecutar trabajos en segundo plano que procesan colas y mensajes.
- Implementar aplicaciones serverless con contenedores que escalan a cero.
- Construir aplicaciones distribuidas usando Dapr para comunicación entre servicios.
- Desplegar aplicaciones web y APIs con escalado automático sin gestión de infraestructura.
- Ejecutar aplicaciones que requieren múltiples protocolos (HTTP, gRPC, WebSockets).
- Implementar arquitecturas de microservicios sin la complejidad de gestionar Kubernetes directamente.

## Errores Comunes

- Pensar que Container Apps requiere gestión de Kubernetes (Azure gestiona Kubernetes, tú solo despliegas contenedores).
- Confundir Container Apps con App Service (Container Apps es para contenedores, App Service es para código).
- Creer que Container Apps es lo mismo que AKS (Container Apps abstrae Kubernetes, AKS te da control completo).
- Asumir que Container Apps siempre tiene instancias ejecutándose (puede escalar a cero cuando no hay tráfico).
- Pensar que Container Apps solo soporta HTTP (soporta HTTP, gRPC, WebSockets y TCP).
- Confundir Revision con versión de contenedor (Revision es una versión de la Container App completa).
- Creer que Container Apps requiere configuración compleja de escalado (las reglas de escalado son simples).
- Asumir que Container Apps es más costoso que App Service (puede ser más económico al escalar a cero).

## Preguntas

1. ¿Azure Container Apps es una plataforma serverless basada en Kubernetes que permite ejecutar microservicios sin gestionar Kubernetes directamente?.

2. ¿Container Apps escala automáticamente desde cero hasta miles de instancias según demanda, eventos o métricas?.

3. ¿Container Apps puede escalar a cero cuando no hay tráfico para reducir costos?.

4. ¿Container Apps soporta múltiples protocolos incluyendo HTTP, gRPC, WebSockets y TCP?.

5. ¿Container App Environment proporciona infraestructura compartida y red para múltiples Container Apps?.

6. ¿Las Revisiones representan versiones inmutables de una Container App que permiten gestión de despliegues?.

7. ¿Container Apps se integra con Dapr para construir aplicaciones distribuidas y resilientes?.

8. ¿Container Apps es adecuado para microservicios, aplicaciones event-driven y trabajos en segundo plano?.
