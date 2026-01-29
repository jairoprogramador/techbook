# Azure Disk Storage

## Analogía

Azure Disk Storage es como tener discos duros físicos que tú mismo gestionas en un almacén compartido. Imagina que necesitas discos para tus servidores virtuales. En lugar de que Azure gestione todo automáticamente (como Managed Disks), tú decides exactamente dónde guardar cada disco: en qué cuenta de almacenamiento, cómo organizarlos, y cómo gestionarlos. Azure Disk Storage funciona igual: son discos que se almacenan en Storage Accounts que tú gestionas manualmente. Tienes más control, pero también más responsabilidad: debes crear las cuentas de almacenamiento, gestionar cómo se distribuyen los discos, y preocuparte por los límites de IOPS y throughput de cada cuenta. Es como la diferencia entre tener un servicio de almacenamiento gestionado (Managed Disks) versus gestionar tu propio almacén (Unmanaged Disks en Storage Accounts).

## Definición

Azure Disk Storage (Unmanaged Disks) es el almacenamiento de discos de máquinas virtuales que se almacenan como blobs de páginas en Azure Storage Accounts y requieren gestión manual de las cuentas de almacenamiento.

Permite:

- Almacenar discos de VMs como blobs de páginas en Storage Accounts gestionadas manualmente.
- Tener control completo sobre dónde y cómo se almacenan los discos.
- Gestionar manualmente la distribución de discos entre múltiples Storage Accounts.
- Crear y gestionar Storage Accounts para organizar discos según necesidades.
- Configurar redundancia a nivel de Storage Account (LRS, GRS, ZRS).
- Gestionar límites de IOPS y throughput por Storage Account manualmente.
- Migrar desde Unmanaged Disks a Managed Disks cuando sea necesario.
- Usar Storage Accounts existentes para almacenar discos de VMs.

## Componentes

**Unmanaged Disk** – Disco de VM almacenado como blob de páginas en una Storage Account gestionada manualmente.

**Page Blob** – Tipo de blob usado para almacenar discos de VMs con acceso aleatorio (hasta 8 TB por blob).

**Storage Account** – Cuenta de almacenamiento que contiene los blobs de páginas (discos) y debe gestionarse manualmente.

**VHD File** – Archivo de disco duro virtual almacenado como blob de páginas en la Storage Account.

**IOPS Limit** – Límite de operaciones de entrada/salida por segundo por Storage Account (20,000 IOPS para Standard).

**Throughput Limit** – Límite de throughput por Storage Account (hasta 20 Gbps dependiendo del tipo).

**Storage Account Distribution** – Distribución manual de discos entre múltiples Storage Accounts para evitar límites.

**LRS (Locally Redundant Storage)** – Redundancia local con replicación tres veces en el mismo centro de datos.

**GRS (Geo-Redundant Storage)** – Redundancia geográfica con replicación en múltiples regiones.

**ZRS (Zone-Redundant Storage)** – Redundancia de zona con replicación en múltiples Availability Zones.

## Funcionalidad

1. Se crea una Storage Account para almacenar los discos de VMs (o se usa una existente).
2. Se crea un disco de VM especificando la Storage Account donde se almacenará.
3. El disco se almacena como un blob de páginas (VHD) dentro de la Storage Account.
4. Se debe gestionar manualmente la distribución de discos entre Storage Accounts para evitar límites.
5. Cada Storage Account tiene límites de IOPS (20,000 para Standard) y throughput que deben considerarse.
6. Se configura redundancia a nivel de Storage Account (LRS, GRS, ZRS) según necesidades.
7. Los discos se asocian a VMs mediante la configuración de la VM especificando la Storage Account y blob.
8. Se pueden crear múltiples Storage Accounts y distribuir discos entre ellas para escalar.
9. Se puede migrar desde Unmanaged Disks a Managed Disks para simplificar la gestión.

## Casos de Uso

- Gestionar discos de VMs cuando se requiere control completo sobre Storage Accounts.
- Usar Storage Accounts existentes para almacenar discos de VMs.
- Distribuir discos entre múltiples Storage Accounts para escalar más allá de límites individuales.
- Migrar VMs existentes que usan Unmanaged Disks sin cambiar a Managed Disks inmediatamente.
- Gestionar discos en escenarios donde se necesita control granular sobre la organización de almacenamiento.
- Usar discos en Storage Accounts con configuraciones específicas de redundancia o ubicación.
- Mantener compatibilidad con implementaciones antiguas que usan Unmanaged Disks.

## Errores Comunes

- Confundir Unmanaged Disks con Managed Disks (Unmanaged requiere gestionar Storage Accounts, Managed es automático).
- Pensar que Unmanaged Disks no tienen límites (cada Storage Account tiene límites de IOPS y throughput).
- Asumir que se pueden almacenar todos los discos en una sola Storage Account (puede alcanzar límites rápidamente).
- Creer que Unmanaged Disks son más simples que Managed Disks (Managed Disks es más simple y recomendado).
- Confundir Page Blob con Block Blob (Page Blobs son para discos, Block Blobs son para archivos).
- Pensar que se puede cambiar fácilmente entre Unmanaged y Managed Disks (requiere migración).
- Asumir que Unmanaged Disks tienen mejor rendimiento (Managed Disks puede tener mejor rendimiento y gestión).
- Creer que Unmanaged Disks es la única opción (Managed Disks es la opción recomendada por Microsoft).

## Preguntas

1. ¿Azure Disk Storage (Unmanaged Disks) almacena discos de VMs como blobs de páginas en Storage Accounts gestionadas manualmente?.

2. ¿Unmanaged Disks requiere crear y gestionar Storage Accounts manualmente a diferencia de Managed Disks que Azure gestiona automáticamente?.

3. ¿Cada Storage Account tiene límites de IOPS (20,000 para Standard) y throughput que deben considerarse al usar Unmanaged Disks?.

4. ¿Los discos Unmanaged se almacenan como Page Blobs (VHD files) dentro de Storage Accounts?.

5. ¿Se debe distribuir manualmente discos entre múltiples Storage Accounts para evitar límites de IOPS y throughput?.

6. ¿Managed Disks es la opción recomendada sobre Unmanaged Disks porque Azure gestiona automáticamente las Storage Accounts?.

7. ¿Unmanaged Disks proporciona más control sobre dónde y cómo se almacenan los discos pero requiere más gestión manual?.

8. ¿Se puede migrar desde Unmanaged Disks a Managed Disks para simplificar la gestión de almacenamiento?.
