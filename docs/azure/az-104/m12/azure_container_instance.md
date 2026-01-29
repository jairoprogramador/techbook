# Azure Container Instances (ACI)

## Analogía

Azure Container Instances es como tener un servicio de alquiler de habitaciones por horas donde solo pagas por el tiempo que realmente usas. Imagina que necesitas ejecutar una tarea específica: procesar un lote de imágenes, ejecutar un script de mantenimiento, o correr una aplicación temporal. En lugar de alquilar un servidor completo por un mes completo cuando solo lo necesitas por unas horas, tienes un servicio que te da exactamente lo que necesitas, cuando lo necesitas, y solo pagas por esos minutos u horas. Azure Container Instances funciona igual: ejecutas contenedores Docker sin tener que gestionar servidores, sin tener que configurar clústeres, sin tener que preocuparte por escalado. Solo dices "ejecuta este contenedor" y Azure lo hace inmediatamente. Cuando termina, se detiene y dejas de pagar. Es la forma más rápida y simple de ejecutar contenedores en Azure.

## Definición

Azure Container Instances (ACI) es un servicio serverless completamente gestionado que permite ejecutar contenedores Docker bajo demanda sin necesidad de gestionar máquinas virtuales, clústeres u orquestación.

Permite:

- Ejecutar contenedores Docker Linux o Windows sin gestionar infraestructura.
- Iniciar contenedores en segundos sin configuración previa de servidores.
- Pagar solo por los recursos de cómputo consumidos mientras el contenedor está ejecutándose.
- Ejecutar contenedores aislados sin necesidad de orquestación o clústeres.
- Integrar con Azure Container Registry para desplegar imágenes privadas.
- Ejecutar tareas de corta duración, trabajos por lotes y aplicaciones event-driven.
- Conectar contenedores a redes virtuales para comunicación con otros recursos.
- Configurar variables de entorno y montar volúmenes para persistencia de datos.

## Componentes

**Container Group** – Agrupación de contenedores que comparten recursos (CPU, memoria) y ciclo de vida.

**Container Image** – Imagen Docker que se ejecuta en ACI (desde Docker Hub, ACR o registros públicos).

**CPU and Memory** – Recursos de cómputo asignados al contenedor (se puede especificar CPU y memoria).

**Restart Policy** – Política que define qué hacer cuando el contenedor termina (Always, OnFailure, Never).

**Environment Variables** – Variables de entorno pasadas al contenedor para configuración.

**Volume Mounts** – Montajes de volúmenes para persistencia de datos (Azure Files, Git repos, secretos).

**Network Profile** – Perfil de red que conecta el contenedor a una Virtual Network.

**Public IP Address** – Dirección IP pública opcional para acceso desde Internet.

**Azure Container Registry Integration** – Integración con ACR para autenticación y despliegue de imágenes privadas.

## Funcionalidad

1. Se crea una instancia de contenedor especificando la imagen Docker (pública o desde ACR).
2. Se configura CPU, memoria y otros recursos según los requisitos del contenedor.
3. Se especifican variables de entorno y montajes de volúmenes si es necesario.
4. Se configura la política de reinicio según el tipo de trabajo (Always para servicios, Never para trabajos).
5. Azure inicia el contenedor en segundos sin necesidad de aprovisionar servidores.
6. El contenedor se ejecuta de forma aislada con los recursos asignados.
7. Se puede acceder al contenedor mediante IP pública o mediante red virtual si está configurada.
8. Cuando el contenedor termina (según la política de reinicio), se detiene automáticamente.
9. Se factura solo por el tiempo que el contenedor estuvo ejecutándose y los recursos consumidos.

## Casos de Uso

- Ejecutar trabajos por lotes y tareas de procesamiento de datos de corta duración.
- Implementar aplicaciones event-driven que se ejecutan bajo demanda.
- Ejecutar scripts de mantenimiento y automatización sin mantener servidores.
- Probar y validar contenedores antes de desplegarlos en producción.
- Ejecutar aplicaciones de microservicios simples sin necesidad de orquestación.
- Implementar trabajos programados que se ejecutan periódicamente.
- Ejecutar contenedores de desarrollo y pruebas sin infraestructura permanente.
- Procesar archivos y datos de forma temporal sin almacenamiento persistente.

## Errores Comunes

- Pensar que ACI requiere gestión de servidores o clústeres (es completamente serverless).
- Confundir ACI con AKS (ACI no tiene orquestación, AKS es Kubernetes gestionado).
- Creer que ACI es adecuado para aplicaciones de larga duración (mejor para tareas cortas o event-driven).
- Asumir que los contenedores en ACI persisten datos después de detenerse (requieren volúmenes montados).
- Pensar que ACI escala automáticamente (cada instancia es independiente, no hay auto-scaling).
- Confundir Container Group con múltiples contenedores orquestados (Container Group comparte recursos, no es orquestación).
- Creer que ACI es más costoso que VMs para cargas de trabajo continuas (ACI es mejor para trabajos intermitentes).
- Asumir que todos los contenedores pueden acceder entre sí automáticamente (cada instancia es aislada).

## Preguntas

1. ¿Azure Container Instances es un servicio serverless que ejecuta contenedores Docker sin gestionar servidores o clústeres?.

2. ¿ACI permite ejecutar contenedores en segundos sin necesidad de aprovisionar infraestructura previamente?.

3. ¿Con ACI se paga solo por los recursos consumidos mientras el contenedor está ejecutándose?.

4. ¿ACI es adecuado para trabajos de corta duración, tareas event-driven y aplicaciones temporales?.

5. ¿Los contenedores en ACI se pueden conectar a redes virtuales mediante Network Profiles?.

6. ¿ACI se integra con Azure Container Registry para desplegar imágenes privadas?.

7. ¿Container Group permite agrupar contenedores que comparten recursos pero no proporciona orquestación?.

8. ¿ACI no escala automáticamente y cada instancia de contenedor es independiente?.
