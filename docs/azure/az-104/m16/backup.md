# Azure Backup

Azure Backup es como tener una copia de seguridad programada de tu oficina en un almacén seguro. Imagina que cada noche (o cuando tú definas) se hace una fotografía de todo: documentos, configuraciones, estado de los equipos. Esas fotos se guardan en un lugar seguro y puedes conservarlas días, meses o años según una política que tú configuras. Si un día borras algo por error, sufres un fallo o te atacan, vas al almacén, eliges la “foto” del momento que quieres recuperar y restauras solo eso: un archivo, un disco o la VM completa. No es tener una oficina gemela (eso es Site Recovery); es tener puntos de restauración en el tiempo a los que volver cuando haga falta. Azure Backup se encarga de crear esas copias según la política que definas y de guardarlas en un almacén (Recovery Services vault) gestionado por Azure.

## Definición

Azure Backup es un servicio de Azure que permite **proteger datos y cargas de trabajo** mediante copias de seguridad programadas, almacenadas en un Recovery Services vault, con políticas de retención configurables y restauración por puntos de recuperación.

Permite:

- Crear y programar copias de seguridad de VMs de Azure, archivos y carpetas, SQL Server, SAP HANA y otras cargas de trabajo
- Almacenar puntos de recuperación en un Recovery Services vault con redundancia configurable
- Definir políticas de backup (frecuencia y retención diaria, semanal, mensual, anual)
- Restaurar desde un punto de recuperación: VM completa, discos, archivos o carpetas
- Proteger cargas de trabajo en Azure y en entornos híbridos (on‑premises)
- Usar soft delete y, opcionalmente, Multi-User Authorization (MUA) para mayor seguridad

## Componentes

**Recovery Services vault** – Recurso de Azure que almacena puntos de recuperación y concentra la configuración de backup (políticas, trabajos, restauraciones)

**Backup policy** – Política que define la frecuencia del backup (diario, semanal, etc.) y la retención (cuánto tiempo se conserva cada punto de recuperación)

**Recovery point** – Punto de recuperación: copia consistente de los datos en un momento dado desde la que se puede restaurar

**Retention** – Retención: cuánto tiempo se conservan los puntos de recuperación (por ejemplo, diarios 7 días, semanales 4 semanas, mensuales 12 meses, anuales 10 años)

**Backup job** – Trabajo de backup que ejecuta Azure Backup según la política (programado o bajo demanda)

**Restore** – Operación de restaurar datos o recursos desde un punto de recuperación (VM completa, discos, archivos)

**Soft delete** – Eliminación temporal de datos de backup; los datos permanecen retenidos un tiempo antes de borrarse de forma definitiva

**MUA (Multi-User Authorization)** – Protección adicional que exige la aprobación de un segundo usuario para operaciones destructivas en el vault

**Backup Agent / Extension** – En VMs de Azure, extensión que permite a Azure Backup realizar el backup; en máquinas locales, agente (MARS) para backup de archivos y carpetas

## Funcionalidad

1. Se crea un Recovery Services vault en una suscripción y región
2. Se configura la redundancia del almacenamiento del vault (LRS, ZRS o GRS)
3. Se crea o se asigna una política de backup que define **frecuencia y retención** (diaria, semanal, mensual, anual)
4. Se habilita el backup del recurso (por ejemplo, VM de Azure) y se asocia la política al vault
5. Azure Backup ejecuta los backups según la programación (y opcionalmente bajo demanda)
6. Los puntos de recuperación se almacenan en el Recovery Services vault según la retención definida
7. Para restaurar, se elige un punto de recuperación y el tipo de restauración (VM completa, discos, archivos)
8. Azure Backup restaura los datos al destino indicado (VM nueva, discos existentes, ubicación de archivos)
9. Opcionalmente se habilita soft delete y MUA para proteger contra borrados accidentales o malintencionados

## Casos de Uso

- Proteger VMs de Azure con backups programados y retención a largo plazo
- Cumplir requisitos de cumplimiento y retención legal (por ejemplo, 7–10 años)
- Recuperar archivos o discos concretos sin restaurar la VM completa
- Proteger cargas de trabajo híbridas (archivos y carpetas en servidores on‑premises) con backup a Azure
- Restaurar tras borrado accidental, ransomware o corrupción de datos
- Migrar datos a Azure restaurando backups en una nueva región o suscripción
- Diferenciar backup (puntos en el tiempo) de recuperación ante desastres (replicación y failover con Site Recovery)

## Errores Comunes

- Confundir Azure Backup con Azure Site Recovery (Backup = puntos de recuperación para restaurar; ASR = replicación y failover para continuidad)
- Pensar que el vault crea los backups solo por existir (hay que habilitar backup en cada recurso y asignar una política)
- Creer que retención y frecuencia son lo mismo (frecuencia = cada cuánto se hace backup; retención = cuánto tiempo se guarda cada punto)
- Asumir que se puede restaurar una VM sin tener en cuenta la región del vault y del destino (la restauración depende del alcance del vault y de la redundancia)
- Ignorar soft delete (si está habilitado, los datos “eliminados” siguen existiendo un tiempo y consumen costo)
- Usar solo retención corta cuando hay requisitos legales de conservación a largo plazo (configurar retención anual en la política)
- Pensar que Backup reemplaza las réplicas de Site Recovery para DR (Backup no hace failover automático; ASR sí)

## Preguntas

1. ¿Azure Backup permite proteger datos y cargas de trabajo mediante copias de seguridad programadas almacenadas en un Recovery Services vault?

2. ¿La política de backup en Azure Backup define la frecuencia (diaria, semanal, etc.) y la retención de los puntos de recuperación?

3. ¿Un punto de recuperación es una copia consistente de los datos en un momento dado desde la que se puede restaurar?

4. ¿Azure Backup se usa para restaurar desde un punto en el tiempo, mientras que Site Recovery se usa para replicación y failover ante desastres?

5. ¿El Recovery Services vault es el recurso que almacena los puntos de recuperación y concentra políticas y trabajos de backup?

6. ¿Se puede restaurar desde un punto de recuperación una VM completa, solo discos o solo archivos/carpetas?

7. ¿La retención en una política de backup define cuánto tiempo se conservan los puntos de recuperación (por ejemplo, diarios 7 días, anuales 10 años)?

8. ¿Soft delete en Azure Backup mantiene los datos de backup eliminados de forma temporal antes de borrarlos definitivamente?
