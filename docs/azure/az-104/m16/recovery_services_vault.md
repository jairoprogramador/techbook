# Recovery Services Vault

Recovery Services Vault es como el edificio que alberga dos servicios distintos bajo el mismo techo: el almacén de copias de seguridad (Azure Backup) y el centro de replicación para desastres (Azure Site Recovery). No es ni el backup ni la replicación en sí; es el contenedor común. Las reglas del edificio —por ejemplo, si las copias se replican a otra región o no— se definen al construirlo y no se pueden cambiar después. Dentro del edificio eliges qué usar: solo backup, solo Site Recovery o ambos. El vault es el recurso que unifica dónde y cómo se guardan y protegen los datos para ambos servicios.

## Definición

Recovery Services Vault es el recurso de Azure que actúa como contenedor y punto de configuración común para Azure Backup y Azure Site Recovery: almacena datos de backup y metadatos de replicación, y concentra opciones de redundancia, seguridad y restauración aplicables a ambos servicios.

Permite:

- Albergar en un mismo vault la configuración y los datos de Azure Backup y de Azure Site Recovery
- Definir la redundancia del almacenamiento (LRS, ZRS o GRS) al crear el vault; esta configuración no puede cambiarse después una vez que hay backups
- Habilitar soft delete y Multi-User Authorization (MUA) a nivel de vault para proteger contra borrados y operaciones destructivas
- Con GRS, permitir restauración en la región secundaria (cross-region restore) sin tener el vault en esa región
- Centralizar permisos y controles de seguridad (RBAC, MUA) para backup y recuperación ante desastres en un único recurso

## Componentes

**Recovery Services Vault** – Recurso regional que contiene la configuración y los datos de Azure Backup y Azure Site Recovery

**Storage redundancy** – Redundancia del almacenamiento del vault: LRS (solo local), ZRS (zonas en la misma región) o GRS (réplica en región secundaria). Se configura al crear el vault y no puede modificarse después si ya hay datos de backup

**LRS (Locally Redundant Storage)** – Tres copias en el mismo centro de datos; menor costo, sin réplica geográfica ni cross-region restore

**ZRS (Zone-Redundant Storage)** – Réplica en tres Availability Zones de la región; sin réplica a otra región

**GRS (Geo-Redundant Storage)** – Réplica en región secundaria; permite cross-region restore y mayor protección ante desastre regional

**Soft delete (vault level)** – Configuración a nivel de vault que mantiene los datos de backup “eliminados” un tiempo adicional (p. ej. 14 días) antes de borrarlos; protege contra borrados accidentales o malintencionados

**MUA (Multi-User Authorization)** – Configuración a nivel de vault que exige la aprobación de un segundo usuario para operaciones destructivas (p. ej. deshabilitar soft delete, eliminar datos de backup)

**Cross-region restore** – Con GRS, posibilidad de restaurar desde la región secundaria sin tener el vault en la región de restauración; útil cuando la región primaria no está disponible

**Vault region** – El vault es un recurso regional; se crea en una región concreta y los datos se almacenan según la redundancia elegida (en la misma región con LRS/ZRS, o también en la secundaria con GRS)

**Private Endpoint (vault)** – Opción a nivel de vault para que el tráfico de backup y restauración (y, en ASR, replicación) use la red privada en lugar de la internet pública; mejora seguridad y cumple requisitos de red aislada

## Funcionalidad

1. Se crea un Recovery Services vault en una suscripción y en una región determinada
2. Al crear el vault se elige la redundancia de almacenamiento (LRS, ZRS o GRS); esta elección no puede cambiarse después si ya existen backups en el vault
3. Opcionalmente se configura soft delete y MUA a nivel de vault para todos los datos protegidos por ese vault
4. Para Azure Backup: se habilitan backups de recursos (VMs, archivos, etc.) y se asocian políticas al vault; los puntos de recuperación se almacenan en el vault
5. Para Azure Site Recovery: se configura la replicación (origen y destino) usando el mismo vault; los metadatos y la coordinación de la replicación se gestionan desde el vault
6. Con GRS, si la región primaria falla, se puede usar cross-region restore para restaurar en la región secundaria
7. Los permisos (RBAC) se asignan sobre el recurso vault para controlar quién puede configurar backup, ASR o realizar restauraciones
8. Opcionalmente se configura un Private Endpoint para el vault para que backup, restauración y replicación usen la red privada
9. Si se necesita otra redundancia (p. ej. pasar de LRS a GRS), no se puede cambiar el vault existente con datos; hay que usar un vault nuevo y reconfigurar backups o replicación

## Casos de Uso

- Usar un único vault para centralizar Azure Backup y Azure Site Recovery en la misma región
- Elegir GRS al crear el vault cuando se requiera restauración en otra región (cross-region restore) o protección ante desastre regional
- Reducir costos con LRS cuando no se necesite réplica geográfica ni cross-region restore
- Habilitar soft delete y MUA en el vault para proteger contra borrados y operaciones destructivas tanto de backup como de ASR
- Restaurar en la región secundaria cuando la primaria no esté disponible (vault con GRS)
- Aplicar permisos y controles de seguridad (RBAC, MUA) de forma centralizada sobre backup y recuperación ante desastres
- Aislar el tráfico de backup y restauración en la red privada usando Private Endpoint en el vault

## Errores Comunes

- Confundir el vault con el servicio de Backup o con Site Recovery (el vault es el contenedor; Backup y ASR son los servicios que usan el vault)
- Pensar que se puede cambiar la redundancia (LRS/GRS/ZRS) del vault después de crear backups (no es posible; hay que usar un vault nuevo y reconfigurar)
- Creer que un vault puede estar en varias regiones (el vault es un recurso regional; GRS replica datos a una región secundaria pero el recurso vault sigue en una región)
- Asumir que cross-region restore está disponible con LRS o ZRS (solo está disponible con GRS)
- Deshabilitar soft delete en el vault sin considerar que se pierde protección para todos los datos de ese vault
- Usar un solo vault para todas las regiones (cada región donde se quiera almacenar datos de backup o ASR suele requerir su propio vault en esa región)

## Preguntas

1. ¿Recovery Services vault es el recurso de Azure que actúa como contenedor común para Azure Backup y Azure Site Recovery?

2. ¿La redundancia de almacenamiento del vault (LRS, ZRS, GRS) se configura al crear el vault y no puede modificarse después si ya hay backups?

3. ¿Con GRS el vault permite cross-region restore cuando la región primaria no está disponible?

4. ¿Soft delete y MUA son configuraciones a nivel de vault que aplican a los datos gestionados por ese vault (backup y ASR)?

5. ¿Para cambiar de LRS a GRS con datos ya existentes hay que crear un vault nuevo y reconfigurar backups o replicación?

6. ¿Un mismo Recovery Services vault puede albergar tanto la configuración y datos de Azure Backup como la de Azure Site Recovery?
