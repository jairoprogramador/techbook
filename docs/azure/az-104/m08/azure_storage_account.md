# Azure Storage Account

## Analogía

Azure Storage Account es como tener una cuenta bancaria para almacenamiento en la nube. Imagina que tienes una cuenta bancaria donde puedes guardar diferentes tipos de cosas: documentos importantes (blobs), mensajes para comunicarte (queues), tablas de datos (tables), archivos compartidos (files), y discos para tus servidores (disks). Azure Storage Account funciona igual: es el contenedor principal que agrupa todos estos diferentes tipos de almacenamiento. Cada cuenta tiene un nombre único que se puede acceder desde cualquier lugar del mundo mediante HTTP/HTTPS. Es como tener una bóveda principal con diferentes secciones para diferentes tipos de datos, pero todo bajo un mismo techo y con las mismas credenciales de seguridad.

## Definición

Azure Storage Account es el recurso fundamental de Azure que proporciona un espacio de nombres único para almacenar y acceder a datos de Azure Storage, incluyendo Blob Storage, Queue Storage, Table Storage, File Storage y Disk Storage.

Permite:

- Crear un espacio de nombres único y accesible globalmente mediante HTTP/HTTPS.
- Almacenar diferentes tipos de datos: blobs, queues, tables, files y disks.
- Configurar redundancia (LRS, ZRS, GRS, GZRS) para protección de datos.
- Elegir entre niveles de rendimiento: Standard (HDD) o Premium (SSD).
- Controlar acceso mediante claves de cuenta, SAS tokens, Azure RBAC o Azure AD.
- Configurar reglas de firewall y redes virtuales para restringir acceso.
- Habilitar características avanzadas como versionado, soft delete y inmutabilidad.
- Escalar automáticamente según necesidades sin límites predefinidos.

## Componentes

**Storage Account Name** – Nombre único globalmente que identifica la cuenta de almacenamiento (3-24 caracteres, solo minúsculas y números).

**Resource Group** – Grupo de recursos donde se crea la cuenta de almacenamiento para organización.

**Location/Region** – Región de Azure donde se almacenan los datos físicamente.

**Performance Tier** – Nivel de rendimiento: Standard (HDD) para costos optimizados o Premium (SSD) para alto rendimiento.

**Redundancy** – Opciones de redundancia: LRS, ZRS, GRS, GZRS, RA-GRS, RA-GZRS.

**Access Tier (Blob)** – Nivel de acceso para blobs: Hot (acceso frecuente), Cool (acceso infrecuente), Archive (almacenamiento a largo plazo).

**Access Keys** – Claves de acceso primaria y secundaria para autenticación mediante claves.

**Shared Access Signature (SAS)** – Tokens de acceso delegado con permisos y tiempo limitados.

**Azure RBAC** – Control de acceso basado en roles para gestionar permisos mediante roles de Azure.

**Network Rules** – Reglas de firewall y redes virtuales para restringir acceso por red.

**Blob Storage** – Almacenamiento de objetos para archivos binarios y de texto (imágenes, videos, documentos).

**Queue Storage** – Almacenamiento de mensajes para comunicación asíncrona entre componentes de aplicaciones.

**Table Storage** – Almacenamiento NoSQL para datos estructurados sin esquema.

**File Storage** – Almacenamiento de archivos compartidos mediante SMB o NFS.

**Disk Storage** – Almacenamiento de discos para VMs (Unmanaged Disks).

## Funcionalidad

1. Se crea una Storage Account especificando nombre único, región, nivel de rendimiento y redundancia.
2. Azure asigna un espacio de nombres único accesible globalmente mediante HTTP/HTTPS.
3. Se configuran reglas de red (firewall y redes virtuales) para restringir acceso si es necesario.
4. Se generan claves de acceso (primaria y secundaria) para autenticación mediante claves.
5. Se pueden crear diferentes tipos de almacenamiento dentro de la cuenta: blobs, queues, tables, files, disks.
6. Se configura el nivel de acceso para blobs (Hot, Cool, Archive) según patrones de uso.
7. Se pueden configurar características avanzadas como versionado, soft delete y políticas de retención.
8. Los datos se replican según la redundancia configurada (LRS, ZRS, GRS, etc.).
9. Se puede acceder a los datos mediante claves de cuenta, SAS tokens, Azure RBAC o Azure AD.

## Casos de Uso

- Almacenar archivos estáticos para aplicaciones web (imágenes, videos, documentos) mediante Blob Storage.
- Implementar comunicación asíncrona entre componentes de aplicaciones mediante Queue Storage.
- Almacenar datos estructurados NoSQL para aplicaciones mediante Table Storage.
- Proporcionar almacenamiento compartido de archivos mediante File Storage.
- Gestionar discos para VMs mediante Disk Storage (Unmanaged Disks).
- Centralizar almacenamiento de datos con un espacio de nombres único y acceso global.
- Configurar diferentes niveles de redundancia según requisitos de disponibilidad y costo.
- Restringir acceso mediante reglas de red y autenticación para seguridad.

## Errores Comunes

- Pensar que Storage Account es solo para blobs (soporta blobs, queues, tables, files y disks).
- Confundir Performance Tier con Access Tier (Performance es Standard/Premium, Access es Hot/Cool/Archive para blobs).
- Creer que el nombre de Storage Account puede tener mayúsculas (solo minúsculas y números, 3-24 caracteres).
- Asumir que todas las Storage Accounts tienen las mismas características (depende del tipo y configuración).
- Pensar que LRS es suficiente para todas las cargas de trabajo (GRS o ZRS pueden ser necesarios).
- Confundir Storage Account con Managed Disks (Storage Account contiene Unmanaged Disks, Managed Disks es gestionado por Azure).
- Creer que se puede cambiar la región después de crear la cuenta (requiere crear nueva cuenta y migrar datos).
- Asumir que Access Tier (Hot/Cool/Archive) aplica a todos los tipos de almacenamiento (solo aplica a Blob Storage).

## Preguntas

1. ¿Azure Storage Account proporciona un espacio de nombres único para almacenar diferentes tipos de datos (blobs, queues, tables, files, disks)?

2. ¿Storage Account es accesible globalmente mediante HTTP/HTTPS usando el nombre único de la cuenta?

3. ¿Storage Account soporta diferentes niveles de redundancia: LRS, ZRS, GRS, GZRS para protección de datos?

4. ¿Performance Tier en Storage Account se refiere a Standard (HDD) o Premium (SSD) mientras Access Tier (Hot/Cool/Archive) solo aplica a Blob Storage?

5. ¿Storage Account permite restringir acceso mediante reglas de firewall, redes virtuales, claves de cuenta, SAS tokens o Azure RBAC?

6. ¿El nombre de Storage Account debe ser único globalmente, tener entre 3-24 caracteres y contener solo minúsculas y números?

7. ¿Storage Account contiene Blob Storage, Queue Storage, Table Storage, File Storage y Disk Storage (Unmanaged Disks)?

8. ¿Storage Account escala automáticamente sin límites predefinidos según las necesidades de almacenamiento?
