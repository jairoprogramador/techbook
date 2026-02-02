# Suscripciones (Azure)

## Analogía

Una suscripción en Azure es como el contrato y la cuenta de facturación con la que tu organización usa Azure: define quién paga, qué límites y cuotas hay, y a qué directorio de identidades (tenant de Entra ID) está ligada. Dentro de una suscripción viven los grupos de recursos y los recursos. Puedes tener varias suscripciones (por departamento, entorno o proyecto) y cada una se factura por separado y puede tener límites y políticas propias. Es el nivel donde se asocian facturación, límites de servicio y, normalmente, permisos administrativos amplios.

## Definición

Una suscripción de Azure es un contrato con Microsoft que agrupa recursos y grupos de recursos bajo una unidad de facturación y límites; está asociada a un tenant de Microsoft Entra ID y puede estar bajo un grupo de administración para aplicar gobernanza de forma jerárquica.

Permite:

- Definir la unidad de facturación: el uso de los recursos de la suscripción se factura a esa suscripción
- Establecer límites y cuotas por suscripción (número de VMs, vCPUs, etc.)
- Asociar la suscripción a un tenant de Entra ID para que las identidades del directorio reciban roles RBAC en la suscripción
- Organizar recursos en grupos de recursos dentro de la suscripción
- Aplicar políticas y permisos a nivel de suscripción para que hereden grupos de recursos y recursos
- Colocar la suscripción bajo un grupo de administración para heredar políticas y permisos

## Componentes

**Facturación** – La suscripción es la unidad a la que se asocia el uso y el cobro; puede tener un plan de facturación (p. ej. Pago por uso, Contrato Enterprise)

**Límites y cuotas** – Límites por suscripción (p. ej. número de redes virtuales, vCPUs por región) que pueden solicitarse para aumentar

**Tenant de Entra ID** – Cada suscripción está ligada a un directorio (tenant) de Entra ID; las identidades de ese tenant pueden recibir roles en la suscripción

**Grupos de recursos** – Contenedores dentro de la suscripción que agrupan recursos; todos los recursos de la suscripción pertenecen a algún grupo de recursos

**Grupo de administración** – La suscripción puede ser miembro de un grupo de administración para heredar políticas y estructura jerárquica

**Roles y permisos** – Se asignan roles RBAC en el ámbito de la suscripción para administradores (Owner, Contributor, Reader, etc.)

## Funcionalidad

1. Se crea o se asigna una suscripción a un tenant de Entra ID (al registrarse en Azure o desde el portal de administración)
2. La suscripción define la unidad de facturación y los límites por defecto
3. Dentro de la suscripción se crean grupos de recursos y recursos; todo el uso se atribuye a la suscripción
4. Se asignan roles RBAC a nivel de suscripción para administrar quién puede crear recursos, asignar permisos o ver costos
5. Se pueden asignar políticas de Azure Policy a la suscripción para que apliquen a todos los grupos de recursos y recursos
6. La suscripción puede colocarse bajo un grupo de administración para heredar políticas del padre
7. Cada suscripción está asociada a un solo tenant de Entra ID; para usar otro tenant hay que transferir la suscripción o usar otra suscripción

## Casos de Uso

- Separar facturación por departamento, proyecto o entorno (prod, dev) usando varias suscripciones
- Aplicar límites y gobernanza por suscripción (políticas, RBAC, presupuestos)
- Asociar una suscripción a un tenant de Entra ID para que solo las identidades de ese directorio administren recursos
- Organizar jerarquía de gobernanza colocando suscripciones bajo grupos de administración
- Delegar administración por suscripción (equipo A en suscripción A, equipo B en suscripción B)
- Usar Cost Management y presupuestos a nivel de suscripción para controlar gasto

## Errores Comunes

- Creer que una suscripción puede estar asociada a varios tenants de Entra ID (cada suscripción está asociada a un solo tenant)
- Confundir suscripción con grupo de recursos (la suscripción es el contenedor de facturación y límites; el grupo de recursos agrupa recursos dentro de la suscripción)
- Pensar que los recursos pueden existir sin suscripción (todo recurso pertenece a un grupo de recursos y por tanto a una suscripción)
- Asumir que mover un recurso entre grupos de recursos cambia la suscripción (el recurso sigue en la misma suscripción; solo cambia de grupo de recursos)
- Olvidar que los límites (vCPUs, redes, etc.) son por suscripción y por región (puede ser necesario solicitar aumento de cuota)

## Preguntas

1. ¿Una suscripción de Azure es la unidad de facturación y límites bajo la que se agrupan grupos de recursos y recursos?

2. ¿Cada suscripción está asociada a un solo tenant de Microsoft Entra ID?

3. ¿Todos los recursos de una suscripción pertenecen a algún grupo de recursos dentro de esa suscripción?

4. ¿Se pueden asignar políticas de Azure Policy a nivel de suscripción para que apliquen a todos los recursos de la suscripción?

5. ¿Una suscripción puede ser miembro de un grupo de administración para heredar gobernanza jerárquica?

6. ¿Los límites y cuotas (p. ej. vCPUs, redes) se aplican por suscripción y por región?
