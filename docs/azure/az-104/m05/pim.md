# PIM (Privileged Identity Management)

PIM es como dar llaves de emergencia que solo se pueden usar cuando las activas y durante un tiempo limitado. En lugar de que un administrador tenga el rol de Owner o Contributor asignado todo el tiempo, se le asigna como "elegible": no tiene permisos hasta que los activa cuando los necesita. Al activar, el rol se vuelve efectivo durante unas horas (por ejemplo, 8) y luego se desactiva solo. Así se reduce el acceso permanente a privilegios y se limita el daño si la cuenta se compromete. Opcionalmente, alguien debe aprobar la activación antes de que el rol se conceda.

## Definición

Privileged Identity Management (PIM) es una capacidad de Microsoft Entra ID (requiere edición Premium P2 o Entra ID Governance) que permite gestionar el acceso con privilegios mediante asignaciones "elegibles" (eligible) en lugar de asignaciones permanentes: el usuario no tiene el rol hasta que lo activa (just-in-time) durante un período limitado; opcionalmente la activación requiere aprobación.

Permite:

- Asignar roles de Azure (RBAC) o roles de Entra ID como "elegibles" en lugar de permanentes: el usuario no tiene permisos hasta que activa el rol
- Acceso just-in-time (JiT): el usuario activa el rol cuando lo necesita; el rol se concede durante un tiempo acotado (p. ej. 8 horas) y luego se revoca automáticamente
- Reducir el acceso privilegiado permanente y limitar el impacto de una cuenta comprometida
- Exigir aprobación antes de activar un rol (workflow de aprobación configurable)
- Aplicar PIM a roles de Azure (suscripción, grupo de recursos, grupo de administración) y a roles de Entra ID (administrador del directorio)
- Auditar activaciones y asignaciones elegibles desde el centro de PIM

## Componentes

**Asignación elegible (eligible assignment)** – Asignación de un rol (Azure RBAC o Entra ID) que no concede permisos hasta que el usuario (o grupo) activa el rol; el usuario puede activar cuando lo necesite, dentro de las reglas configuradas

**Asignación activa (active assignment)** – Asignación que concede el rol de forma permanente o temporal; en PIM, al "activar" un rol elegible se crea temporalmente una asignación activa que expira al terminar el tiempo de activación

**Activación (activation)** – Acción por la que un usuario con asignación elegible solicita que el rol se conceda; opcionalmente requiere aprobación; una vez concedido, el rol está activo durante el tiempo configurado (duración máxima de activación)

**Just-in-time (JiT)** – Modelo de acceso en el que los privilegios se conceden solo cuando se activan y durante un período limitado, en lugar de tenerlos asignados de forma permanente

**Duración máxima de activación** – Tiempo máximo que el rol permanece activo tras una activación (p. ej. 8 horas); al expirar, la asignación activa se revoca automáticamente

**Aprobación** – Flujo opcional en el que uno o más aprobadores deben aprobar la solicitud de activación antes de que el rol se conceda

**PIM para recursos de Azure** – Uso de PIM para roles RBAC en ámbito de grupo de administración, suscripción o grupo de recursos (no a nivel de recurso individual); las asignaciones elegibles se crean desde IAM o desde el centro de PIM

**PIM para roles de Entra ID** – Uso de PIM para roles del directorio (Global Administrator, User Administrator, etc.); las asignaciones elegibles se gestionan desde el centro de PIM en Entra ID

**Requisito de licencia** – Microsoft Entra ID Premium P2 o licencia de Entra ID Governance para usar PIM

## Funcionalidad

1. Se habilita PIM en el tenant (requiere Entra ID Premium P2 o Entra ID Governance)
2. Se asignan roles como "elegibles" a usuarios o grupos: en recursos de Azure (IAM → Add role assignment → tipo "Privileged Identity Management" / Eligible) o en roles de Entra ID (centro de PIM → Entra ID roles → Add assignments)
3. Se configura la duración máxima de activación y opcionalmente la aprobación (uno o más aprobadores) para cada rol o tipo de asignación
4. El usuario que tiene una asignación elegible no tiene permisos hasta que va a "My roles" (o equivalente) y activa el rol; opcionalmente debe justificar y esperar la aprobación
5. Una vez activado (y aprobado si aplica), el rol se concede durante el tiempo configurado; al expirar, la asignación activa se revoca automáticamente
6. Las asignaciones elegibles no se pueden crear para entidades de servicio, identidades administradas o aplicaciones (no pueden realizar el paso de activación); solo para usuarios y grupos
7. En recursos de Azure, las asignaciones elegibles se crean en ámbito de grupo de administración, suscripción o grupo de recursos; no a nivel de recurso individual
8. Se puede auditar quién activó qué rol y cuándo desde el centro de PIM

## Casos de Uso

- Reducir el acceso privilegiado permanente: asignar Owner o Contributor como elegible en lugar de permanente
- Acceso just-in-time para tareas administrativas puntuales (activar el rol solo cuando se necesita)
- Exigir aprobación para activar roles sensibles (p. ej. Global Administrator, User Access Administrator)
- Cumplir requisitos de seguridad y auditoría (quién tuvo privilegios y cuándo)
- Gestionar privilegios para roles de Entra ID (administradores del directorio) y para roles de Azure (suscripción, grupo de recursos) desde un mismo modelo (elegible + activación)

## Errores Comunes

- Confundir asignación elegible con asignación activa (elegible = no tiene el rol hasta que activa; activa = tiene el rol ya concedido)
- Pensar que PIM está incluido en Entra ID Free o Premium P1 (requiere Premium P2 o Entra ID Governance)
- Crear asignaciones elegibles para una entidad de servicio o identidad administrada (no pueden activar; solo usuarios y grupos)
- Crear asignaciones elegibles a nivel de recurso individual en Azure (PIM para Azure roles aplica a grupo de administración, suscripción o grupo de recursos, no a recurso)
- Creer que al activar un rol elegible el rol es permanente (la activación es temporal; expira según la duración máxima configurada)
- Olvidar configurar aprobación cuando se requiere (si la política exige aprobación, hay que designar aprobadores)

## Preguntas

1. ¿PIM (Privileged Identity Management) permite asignar roles como "elegibles" de modo que el usuario no tiene el rol hasta que lo activa (just-in-time)?

2. ¿La activación de un rol elegible concede el rol solo durante un tiempo limitado (duración máxima de activación), tras el cual se revoca automáticamente?

3. ¿PIM requiere Microsoft Entra ID Premium P2 o licencia de Entra ID Governance?

4. ¿Las asignaciones elegibles en PIM no se pueden crear para entidades de servicio ni identidades administradas (solo usuarios y grupos)?

5. ¿En recursos de Azure, las asignaciones elegibles de PIM se pueden crear en ámbito de grupo de administración, suscripción o grupo de recursos, pero no a nivel de recurso individual?

6. ¿PIM puede exigir aprobación de uno o más aprobadores antes de conceder el rol al activar?
