# Azure Kubernetes Service (AKS)

## Analogía

Azure Kubernetes Service es como tener un equipo completo de trabajadores especializados que gestionan una fábrica compleja, pero Azure se encarga de contratar y entrenar a los supervisores. Imagina que tienes una fábrica enorme con cientos de máquinas que necesitan coordinación perfecta: cuándo encender cada máquina, cómo distribuir el trabajo, cómo manejar fallos, cómo escalar cuando hay más pedidos. Kubernetes es como el sistema de gestión de esa fábrica: coordina todo automáticamente. AKS es Azure diciendo: "Yo contrato y entreno a los supervisores (el plano de control), tú solo gestionas a los trabajadores (los nodos y aplicaciones)". Tienes control completo sobre cómo funciona tu fábrica, pero Azure se encarga de la parte más compleja: mantener a los supervisores funcionando, actualizados y seguros. Es Kubernetes con la complejidad reducida, pero manteniendo todo el poder.

## Definición

Azure Kubernetes Service (AKS) es un servicio de Kubernetes gestionado que proporciona un plano de control gestionado por Azure mientras el usuario gestiona los nodos de trabajo y las cargas de trabajo.

Permite:

- Ejecutar clústeres de Kubernetes sin gestionar el plano de control (master nodes).
- Desplegar y gestionar aplicaciones en contenedores usando la API completa de Kubernetes.
- Escalar nodos y pods automáticamente según demanda y métricas.
- Integrar con servicios de Azure mediante identidades gestionadas y controladores.
- Gestionar actualizaciones del plano de control y nodos mediante Azure.
- Implementar arquitecturas de microservicios complejas con orquestación completa.
- Usar cualquier protocolo de red (HTTP, TCP, UDP) y configuración personalizada.
- Conectar clústeres a redes virtuales para integración con otros recursos de Azure.

## Componentes

**Control Plane (Managed)** – Plano de control de Kubernetes gestionado por Azure (API server, etcd, scheduler, controller manager).

**Node Pool** – Grupo de nodos de trabajo (VMs) que ejecutan los pods y cargas de trabajo.

**Pod** – Unidad más pequeña de despliegue en Kubernetes que contiene uno o más contenedores.

**Service** – Abstracción que expone aplicaciones ejecutándose en pods mediante IP estable y balanceo de carga.

**Deployment** – Recurso que gestiona réplicas de pods y actualizaciones graduales.

**Ingress Controller** – Controlador que gestiona tráfico HTTP/HTTPS entrante y enrutamiento.

**Namespace** – Agrupación lógica que aísla recursos dentro del clúster.

**Azure CNI** – Plugin de red que integra pods directamente con redes virtuales de Azure.

**Managed Identity** – Identidad gestionada que permite a pods acceder a servicios de Azure sin credenciales.

**Horizontal Pod Autoscaler (HPA)** – Componente que escala pods automáticamente según métricas (CPU, memoria, personalizadas).

**Cluster Autoscaler** – Componente que escala nodos automáticamente según demanda de pods.

## Funcionalidad

1. Se crea un clúster AKS especificando la versión de Kubernetes y configuración inicial.
2. Azure crea y gestiona el plano de control (control plane) automáticamente.
3. Se crean node pools con nodos de trabajo (VMs) que ejecutarán los pods.
4. Se despliegan aplicaciones usando manifiestos YAML o herramientas como kubectl.
5. Kubernetes orquesta los pods distribuyéndolos en los nodos disponibles.
6. Los Services exponen aplicaciones mediante IPs estables y balanceo de carga.
7. HPA escala pods automáticamente según métricas configuradas (CPU, memoria).
8. Cluster Autoscaler escala nodos automáticamente cuando hay demanda de recursos.
9. Azure gestiona actualizaciones del plano de control y permite actualizar nodos mediante operaciones controladas.

## Casos de Uso

- Implementar arquitecturas de microservicios complejas que requieren orquestación completa.
- Desplegar aplicaciones que necesitan acceso completo a la API de Kubernetes.
- Ejecutar cargas de trabajo que requieren protocolos personalizados (TCP, UDP) y configuración avanzada.
- Implementar aplicaciones que necesitan escalado automático complejo basado en métricas personalizadas.
- Gestionar aplicaciones distribuidas que requieren coordinación entre múltiples servicios.
- Integrar con ecosistemas de Kubernetes existentes y herramientas de la comunidad.
- Implementar aplicaciones que requieren características avanzadas de Kubernetes (StatefulSets, DaemonSets).
- Migrar aplicaciones existentes de Kubernetes on-premises a Azure.

## Errores Comunes

- Pensar que AKS gestiona completamente el clúster (solo gestiona el plano de control, tú gestionas los nodos).
- Confundir AKS con Container Apps (AKS da control completo de Kubernetes, Container Apps abstrae Kubernetes).
- Creer que AKS es más simple que Kubernetes on-premises (sigue siendo complejo, Azure solo gestiona el plano de control).
- Asumir que AKS escala automáticamente sin configuración (requiere configurar HPA y Cluster Autoscaler).
- Pensar que los pods persisten datos automáticamente (requiere PersistentVolumes para almacenamiento persistente).
- Confundir Service con Ingress (Service expone pods, Ingress gestiona tráfico HTTP/HTTPS entrante).
- Creer que AKS es adecuado para todas las aplicaciones (Container Apps puede ser más simple para casos básicos).
- Asumir que AKS no requiere conocimientos de Kubernetes (requiere conocimiento significativo de Kubernetes).

## Preguntas

1. ¿Azure Kubernetes Service gestiona el plano de control de Kubernetes mientras el usuario gestiona los nodos de trabajo?.

2. ¿AKS proporciona acceso completo a la API de Kubernetes para desplegar y gestionar aplicaciones?.

3. ¿AKS permite escalar pods automáticamente mediante Horizontal Pod Autoscaler (HPA) según métricas?.

4. ¿Cluster Autoscaler en AKS escala nodos automáticamente cuando hay demanda de recursos para pods?.

5. ¿AKS integra pods con redes virtuales de Azure mediante Azure CNI para comunicación con otros recursos?.

6. ¿AKS es adecuado para arquitecturas de microservicios complejas que requieren orquestación completa?.

7. ¿AKS requiere conocimiento de Kubernetes y gestión de nodos, a diferencia de Container Apps que abstrae Kubernetes?.

8. ¿AKS permite usar cualquier protocolo de red (HTTP, TCP, UDP) y configuración personalizada de Kubernetes?.
