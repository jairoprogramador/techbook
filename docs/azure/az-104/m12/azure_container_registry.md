# Azure Container Registry (ACR)

## Analogía

Azure Container Registry es como tener un almacén privado y seguro para tus contenedores Docker. Imagina que eres un chef y creas recetas especiales (imágenes de contenedores). En lugar de compartir tus recetas públicamente donde cualquiera puede copiarlas, tienes un almacén privado con seguridad de banco donde guardas tus recetas secretas. Solo las personas autorizadas pueden acceder. Cuando necesitas cocinar (ejecutar un contenedor), vas al almacén, tomas la receta exacta que necesitas, y la usas. Azure Container Registry funciona igual: es un repositorio privado donde almacenas tus imágenes de contenedores Docker. Solo tú y quienes autorices pueden acceder. Cuando Azure Container Instances, Container Apps o AKS necesitan ejecutar un contenedor, van al registro, descargan la imagen, y la ejecutan. Es como Docker Hub pero privado, seguro y completamente integrado con Azure.

## Definición

Azure Container Registry (ACR) es un servicio de registro privado gestionado basado en Docker Registry que permite almacenar, gestionar y desplegar imágenes de contenedores Docker de forma segura.

Permite:

- Almacenar imágenes de contenedores Docker de forma privada y segura.
- Gestionar versiones de imágenes mediante tags y etiquetas.
- Autenticar y autorizar acceso mediante Entra ID e identidades gestionadas.
- Integrar con servicios de Azure (ACI, Container Apps, AKS) para despliegue automático.
- Escanear imágenes en busca de vulnerabilidades de seguridad automáticamente.
- Replicar imágenes en múltiples regiones para disponibilidad y rendimiento.
- Gestionar políticas de retención para limpiar imágenes antiguas automáticamente.
- Integrar con pipelines CI/CD para construcción y despliegue automatizado de imágenes.

## Componentes

**Registry** – Instancia del registro que almacena las imágenes de contenedores (básico, estándar, premium).

**Repository** – Repositorio que contiene todas las versiones de una imagen específica.

**Image** – Imagen de contenedor Docker almacenada en el registro.

**Tag** – Etiqueta que identifica una versión específica de una imagen (ej: v1.0, latest).

**Manifest** – Metadatos que describen una imagen incluyendo capas, tamaño y configuración.

**Entra ID Authentication** – Autenticación mediante Entra ID para acceso seguro.

**Managed Identity** – Identidad gestionada que permite a servicios de Azure acceder al registro sin credenciales.

**Webhooks** – Notificaciones automáticas cuando se realizan acciones en el registro (push, delete).

**Geographic Replication** – Replicación de imágenes en múltiples regiones para disponibilidad global.

**Security Scanning** – Escaneo automático de imágenes en busca de vulnerabilidades de seguridad.

**Retention Policies** – Políticas que definen cuánto tiempo mantener imágenes antes de eliminarlas.

## Funcionalidad

1. Se crea un Azure Container Registry especificando el nombre, región y SKU (básico, estándar, premium).
2. Se autentica con el registro mediante Azure AD, Managed Identity o credenciales de administrador.
3. Se construyen imágenes de contenedores localmente o mediante Azure Container Registry Tasks.
4. Se envían imágenes al registro mediante `docker push` o herramientas de Azure.
5. Las imágenes se almacenan con tags que identifican versiones específicas.
6. Se configuran políticas de retención para gestionar automáticamente imágenes antiguas.
7. Los servicios de Azure (ACI, Container Apps, AKS) se autentican y descargan imágenes del registro.
8. Se pueden replicar imágenes en múltiples regiones para disponibilidad y rendimiento.
9. El registro escanea automáticamente las imágenes en busca de vulnerabilidades de seguridad.

## Casos de Uso

- Almacenar imágenes de contenedores privadas para aplicaciones empresariales.
- Gestionar versiones de imágenes mediante tags para control de versiones.
- Integrar con pipelines CI/CD para construcción y despliegue automatizado.
- Proporcionar imágenes a ACI, Container Apps y AKS para despliegue de aplicaciones.
- Escanear imágenes en busca de vulnerabilidades antes de desplegarlas en producción.
- Replicar imágenes en múltiples regiones para reducir latencia y mejorar disponibilidad.
- Gestionar políticas de retención para limpiar automáticamente imágenes antiguas y reducir costos.
- Autenticar acceso mediante Azure AD para seguridad empresarial.

## Errores Comunes

- Pensar que ACR es público como Docker Hub (ACR es privado por defecto, requiere autenticación).
- Confundir Registry con Repository (Registry es la instancia completa, Repository contiene una imagen específica).
- Creer que las imágenes se almacenan indefinidamente (se pueden configurar políticas de retención).
- Asumir que ACR solo funciona con servicios de Azure (se puede usar desde cualquier lugar con autenticación).
- Pensar que todas las SKUs de ACR tienen las mismas características (Premium tiene más características).
- Confundir tags con versiones (tags son etiquetas, pueden ser cualquier cosa, no solo números de versión).
- Creer que ACR construye imágenes automáticamente (requiere Azure Container Registry Tasks o construcción externa).
- Asumir que las imágenes se replican automáticamente (la replicación geográfica requiere configuración en SKU Premium).

## Preguntas

1. ¿Azure Container Registry es un servicio de registro privado que almacena imágenes de contenedores Docker de forma segura?.

2. ¿ACR autentica acceso mediante Entra ID e identidades gestionadas para seguridad?.

3. ¿ACR se integra con ACI, Container Apps y AKS para desplegar imágenes automáticamente?.

4. ¿Los tags en ACR identifican versiones específicas de imágenes pero pueden ser cualquier etiqueta, no solo números?.

5. ¿ACR puede escanear imágenes automáticamente en busca de vulnerabilidades de seguridad?.

6. ¿La replicación geográfica en ACR Premium replica imágenes en múltiples regiones para disponibilidad global?.

7. ¿ACR permite configurar políticas de retención para limpiar automáticamente imágenes antiguas?.

8. ¿ACR se integra con pipelines CI/CD mediante Azure Container Registry Tasks para construcción automatizada?.
