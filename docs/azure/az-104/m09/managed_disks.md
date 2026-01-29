# Managed Disks

## Analogía

Managed Disks es como tener un servicio de almacenamiento completamente gestionado donde no tienes que preocuparte por los detalles técnicos. Imagina que necesitas almacenar archivos importantes. En lugar de comprar discos físicos, conectarlos, configurarlos, hacer backups manuales y preocuparte por su mantenimiento, tienes un servicio que hace todo eso por ti. Solo le dices "necesito 100 GB de almacenamiento" y el servicio se encarga de todo: compra los discos, los configura, los respalda automáticamente, los mantiene actualizados, y si algo falla, los reemplaza sin que tú te enteres. Managed Disks funciona igual: Azure gestiona completamente el almacenamiento de tus VMs. No tienes que crear cuentas de almacenamiento, gestionar blobs, o preocuparte por la redundancia. Solo especificas el tamaño y tipo de disco, y Azure hace el resto.

## Definición

Managed Disks es el servicio de almacenamiento gestionado de Azure que simplifica la gestión de discos de máquinas virtuales eliminando la necesidad de gestionar cuentas de almacenamiento y proporcionando redundancia automática.

Permite:

- Crear y gestionar discos sin necesidad de crear cuentas de almacenamiento manualmente
- Elegir entre diferentes tipos de discos según rendimiento (Standard HDD, Standard SSD, Premium SSD, Ultra Disks)
- Configurar redundancia automática (LRS, ZRS, GRS) sin configuración manual
- Escalar automáticamente el tamaño del disco según necesidades
- Realizar snapshots y backups de discos de forma sencilla
- Migrar fácilmente entre diferentes tipos de discos
- Gestionar automáticamente la distribución de discos en cuentas de almacenamiento
- Proteger contra pérdida de datos mediante replicación automática

## Componentes

**OS Disk** – Disco del sistema operativo que contiene el sistema operativo y se usa para arrancar la VM

**Data Disk** – Disco de datos adicional conectado a la VM para almacenar datos de aplicaciones

**Disk Type** – Tipo de disco según rendimiento: Standard HDD, Standard SSD, Premium SSD, Ultra Disks

**Disk Size** – Tamaño del disco que determina capacidad y rendimiento (IOPS y throughput)

**LRS (Locally Redundant Storage)** – Replicación de datos tres veces dentro del mismo centro de datos

**ZRS (Zone-Redundant Storage)** – Replicación sincrónica en tres Availability Zones

**GRS (Geo-Redundant Storage)** – Replicación en múltiples regiones para protección geográfica

**Snapshot** – Copia puntual de un disco en un momento específico

**Disk SKU** – Especificación del disco que define tipo, tamaño y rendimiento

## Funcionalidad

1. Se crea un Managed Disk especificando el tipo (Standard HDD, Standard SSD, Premium SSD) y tamaño.
2. Azure gestiona automáticamente la creación y distribución del disco en cuentas de almacenamiento.
3. El disco se asocia a una VM como OS Disk o Data Disk según la configuración.
4. Azure replica automáticamente los datos según la redundancia configurada (LRS por defecto).
5. Se pueden crear snapshots del disco en cualquier momento para backups o clonación.
6. El tamaño del disco se puede aumentar sin downtime (solo requiere reinicio en algunos casos).
7. Se puede migrar entre diferentes tipos de discos (Standard a Premium) según necesidades de rendimiento.
8. Azure gestiona automáticamente la distribución de discos para evitar límites de cuentas de almacenamiento.
9. Los discos se pueden desasociar de una VM y asociarse a otra sin pérdida de datos.

## Casos de Uso

- Simplificar gestión de almacenamiento de VMs sin necesidad de crear cuentas de almacenamiento manualmente.
- Mejorar rendimiento usando Premium SSD o Ultra Disks para aplicaciones que requieren alto IOPS.
- Reducir costos usando Standard HDD para cargas de trabajo que no requieren alto rendimiento.
- Implementar alta disponibilidad usando ZRS para discos críticos distribuidos en Availability Zones.
- Realizar backups mediante snapshots de discos para recuperación ante desastres.
- Escalar capacidad de almacenamiento aumentando el tamaño de discos según necesidades.
- Migrar entre tipos de discos para optimizar costos y rendimiento.
- Proteger datos mediante replicación automática sin configuración manual.

## Errores Comunes

- Pensar que Managed Disks requiere crear cuentas de almacenamiento manualmente (Azure las gestiona automáticamente).
- Confundir Managed Disks con Unmanaged Disks (Managed es más simple y recomendado).
- Creer que se puede cambiar el tipo de disco sin recrear (requiere migración o recreación).
- Asumir que todos los tipos de discos tienen el mismo rendimiento (Premium SSD tiene mayor IOPS que Standard).
- Pensar que LRS es suficiente para todas las cargas de trabajo (ZRS o GRS pueden ser necesarios para alta disponibilidad).
- Confundir tamaño de disco con rendimiento (tamaño mayor no siempre significa mayor rendimiento).
- Creer que se puede reducir el tamaño de un disco (solo se puede aumentar, no reducir).
- Asumir que Managed Disks y Storage Accounts son lo mismo (Managed Disks usa Storage Accounts internamente pero los gestiona Azure).

## Preguntas

1. ¿Managed Disks elimina la necesidad de crear y gestionar cuentas de almacenamiento manualmente?

2. ¿Los tipos de discos incluyen Standard HDD, Standard SSD, Premium SSD y Ultra Disks según rendimiento necesario?

3. ¿LRS replica datos tres veces dentro del mismo centro de datos proporcionando redundancia local?

4. ¿ZRS replica datos sincrónicamente en tres Availability Zones para protección contra fallos de zona?

5. ¿Se puede aumentar el tamaño de un Managed Disk pero no reducirlo?

6. ¿Se pueden crear snapshots de Managed Disks para backups y clonación de VMs?

7. ¿Premium SSD proporciona mayor IOPS y throughput comparado con Standard HDD o Standard SSD?

8. ¿Azure gestiona automáticamente la distribución de Managed Disks en cuentas de almacenamiento para evitar límites?
