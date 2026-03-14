# Azure File Storage

Azure File Storage es como tener una unidad de red compartida en la nube que funciona exactamente igual que las carpetas compartidas que usas en tu oficina. Imagina que en tu oficina tienes una carpeta compartida en un servidor donde todos pueden guardar y acceder a archivos. Azure File Storage funciona igual, pero en lugar de estar en un servidor físico en tu oficina, está en la nube de Azure. Puedes montarla en Windows como si fuera una unidad de red normal (como Z:\), o en Linux como si fuera un sistema de archivos normal. Lo mejor es que puedes acceder a ella desde cualquier lugar: desde VMs en Azure, desde servidores on-premises, o incluso desde tu computadora personal. Es como tener un disco duro compartido en la nube que se comporta exactamente como un disco duro local, pero accesible desde cualquier lugar con las credenciales correctas.

## Definición

Azure File Storage es un servicio de almacenamiento de archivos compartidos que permite crear recursos compartidos de archivos accesibles mediante protocolos SMB (Server Message Block) o NFS (Network File System) sin necesidad de gestionar servidores.

Permite:

- Crear recursos compartidos de archivos accesibles mediante protocolos estándar SMB o NFS.
- Montar recursos compartidos directamente en VMs Windows o Linux sin servidores intermedios.
- Acceder a archivos desde múltiples VMs simultáneamente como si fuera almacenamiento local.
- Integrar con Entra ID para autenticación y control de acceso basado en identidad.
- Sincronizar recursos compartidos con servidores on-premises mediante Azure File Sync.
- Elegir entre almacenamiento Standard o Premium según requisitos de rendimiento.
- Configurar redundancia (LRS, ZRS, GRS) para protección contra pérdida de datos.
- Acceder a recursos compartidos desde cualquier lugar con conectividad a Azure.
- Acceso seguro con Active Directory Domain Services (AD DS) local, Microsoft Entra Domain Services, Azure RBAC y Claves de cuenta de almacenamiento.

## Componentes

**File Share** – Recurso compartido de archivos que se monta como unidad de red o sistema de archivos.

**Storage Account** – Cuenta de almacenamiento que contiene los recursos compartidos de archivos.

**SMB Protocol** – Protocolo Server Message Block usado principalmente por Windows para recursos compartidos de archivos.

**NFS Protocol** – Protocolo Network File System usado principalmente por Linux para sistemas de archivos de red.

**Storage Tier** – Nivel de almacenamiento: Standard (HDD) o Premium (SSD) según rendimiento necesario.

**Access Tier** – Nivel de acceso: Hot (acceso frecuente), Cool (acceso infrecuente), Transaction Optimized (optimizado para transacciones).

**Azure File Sync** – Servicio que sincroniza recursos compartidos de Azure Files con servidores Windows Server on-premises.

**Active Directory Integration** – Integración con Entra ID o AD DS para autenticación y control de acceso.

**Snapshot** – Copia puntual de un recurso compartido en un momento específico para backup.

**Quota** – Límite de tamaño máximo configurado para un recurso compartido.

## Funcionalidad

1. Se crea una cuenta de almacenamiento con soporte para Azure Files habilitado.
2. Se crea un recurso compartido de archivos especificando el protocolo (SMB o NFS) y el nivel de almacenamiento.
3. Se configura el tamaño del recurso compartido (quota) y el nivel de acceso según el uso esperado.
4. Para SMB, se configura autenticación mediante Entra ID o Active Directory Domain Services.
5. Para NFS, se configura acceso basado en red mediante reglas de firewall y redes virtuales.
6. Se monta el recurso compartido en VMs Windows usando SMB o en VMs Linux usando NFS.
7. Los archivos se almacenan en el recurso compartido y son accesibles desde todas las VMs que lo montaron.
8. Se pueden crear snapshots del recurso compartido para backups y recuperación.
9. Opcionalmente, se configura Azure File Sync para sincronizar con servidores on-premises.

## Casos de Uso

- Compartir archivos entre múltiples VMs en Azure como almacenamiento compartido.
- Migrar recursos compartidos de archivos desde servidores on-premises a Azure.
- Almacenar perfiles de usuario y datos de aplicaciones compartidas en entornos de escritorio virtual.
- Compartir archivos de configuración y datos entre aplicaciones distribuidas.
- Crear backups de archivos mediante snapshots programados.
- Sincronizar archivos entre Azure y servidores on-premises mediante Azure File Sync.
- Almacenar datos de aplicaciones que requieren acceso de archivo compartido (SQL Server, aplicaciones .NET).
- Proporcionar almacenamiento compartido para aplicaciones Linux mediante NFS.

## Errores Comunes

- Pensar que Azure File Storage requiere un servidor de archivos (es serverless, se monta directamente).
- Confundir SMB con NFS (SMB es para Windows, NFS es para Linux; no se pueden usar ambos simultáneamente en el mismo recurso compartido).
- Creer que se puede cambiar el protocolo de un recurso compartido existente (requiere crear un nuevo recurso compartido).
- Asumir que NFS está disponible en todos los niveles de almacenamiento (solo disponible en Premium con LRS o ZRS).
- Pensar que el puerto 445 (SMB) está abierto por defecto en todas las redes (muchas organizaciones lo bloquean).
- Confundir Azure File Storage con Blob Storage (File Storage es para recursos compartidos, Blob Storage es para objetos).
- Creer que Azure File Sync funciona con NFS (solo funciona con SMB).
- Asumir que todos los niveles de redundancia están disponibles para todos los protocolos (NFS requiere LRS o ZRS).

## Preguntas

1. ¿Azure File Storage permite crear recursos compartidos de archivos accesibles mediante protocolos SMB o NFS sin gestionar servidores?.

2. ¿SMB es el protocolo usado principalmente por Windows mientras NFS es usado principalmente por Linux?.

3. ¿Un recurso compartido de Azure Files no puede ser accedido simultáneamente por SMB y NFS (solo uno u otro)?.

4. ¿NFS en Azure Files solo está disponible en almacenamiento Premium con redundancia LRS o ZRS?.

5. ¿Azure File Sync sincroniza recursos compartidos de Azure Files con servidores Windows Server on-premises usando solo SMB?.

6. ¿Azure File Storage se puede montar directamente en VMs Windows o Linux como si fuera almacenamiento local?.

7. ¿Los snapshots de Azure File Storage permiten crear copias puntuales de recursos compartidos para backups?.

8. ¿Azure File Storage integra con Entra ID para autenticación y control de acceso basado en identidad?.
