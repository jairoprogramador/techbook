# Control de Acceso Basado en Roles (RBAC)

RBAC en Azure es como el sistema de control de acceso de un edificio: no das llave maestra a todo el mundo, sino que asignas **quién** (una persona o grupo) puede hacer **qué** (ver, modificar, administrar) **dónde** (un piso, un ala o todo el edificio). El "qué" lo defines mediante **roles**: por ejemplo, "lector" solo ve, "operador de servidores" toca solo servidores, "operador de red" solo redes. Así, si quieres que un equipo administre las máquinas pero no toque la red, usas el rol "Virtual Machine Contributor" en la suscripción: RBAC se encarga de que tengan permiso para VMs y no para la infraestructura de red. El concepto central es RBAC como sistema; el rol es una pieza que define los permisos dentro de ese sistema.

## Definición

Azure RBAC (Control de Acceso Basado en Roles) es el sistema de autorización de Azure que permite gestionar el acceso a los recursos mediante la asignación de roles a identidades en un ámbito determinado.

Permite:

- Controlar quién puede hacer qué en cada ámbito (**recurso, grupo de recursos, suscripción o grupo de administración**). 
- Asignar permisos mediante roles (predefinidos o personalizados) en lugar de permisos sueltos por usuario
- Aplicar el principio de mínimo privilegio limitando el ámbito.
- Centralizar la gestión de acceso: quién (principal), qué (rol) y dónde (ámbito)
- Auditar y revisar asignaciones de acceso de forma coherente en todo Azure

## Componentes

**RBAC** – Sistema completo: definiciones de roles, asignaciones y evaluación de permisos en cada solicitud

**Rol (Role Definition)** – Componente de RBAC: conjunto de permisos (Actions, NotActions, DataActions, NotDataActions) que define qué operaciones permite

**Asignación de rol (Role Assignment)** – Componente de RBAC: vincula un rol a una identidad en un ámbito (quién tiene qué rol y dónde)

**Ámbito (Scope)** – Componente de RBAC: nivel donde aplica la asignación (Management Group, Subscription, Resource Group o Resource)

**Principal** – Identidad que recibe el rol en RBAC: **usuario, grupo, Service Principal o Managed Identity**.

**Roles predefinidos (ejemplos)** – Owner (acceso total y asignar roles), Contributor (gestionar recursos, no asignar roles), Reader (solo ver), User Access Administrator (gestionar acceso), Virtual Machine Contributor (VMs sin red ni storage), Virtual Machine Administrator Login (iniciar sesión en VMs), Network Contributor (solo redes), Storage Account Contributor (cuentas de almacenamiento)

## Funcionalidad

1. RBAC recibe cada solicitud sobre un recurso de Azure (crear, leer, modificar, eliminar, asignar roles)
2. Se identifica el principal (quién hace la solicitud) y el ámbito del recurso afectado
3. RBAC busca todas las asignaciones de roles que apliquen a ese principal en ese ámbito (o ámbitos superiores que incluyan el recurso)
4. Cada asignación aporta un rol; el rol define los permisos (actions) permitidos
5. RBAC combina los permisos de todas las asignaciones aplicables (se suman)
6. Si la operación solicitada está en los permisos efectivos, RBAC autoriza; si no, deniega
7. Las denegaciones explícitas (cuando existan) tienen prioridad sobre permisos concedidos
8. Para dar acceso se crea una asignación de rol: principal + rol + ámbito

## Casos de Uso

- Usar RBAC para dar a un equipo permiso solo sobre VMs en una suscripción sin tocar la red: asignar **Virtual Machine Contributor**
- Delegar la gestión de quién tiene acceso sin tocar recursos: asignar **User Access Administrator**
- Auditoría o soporte con solo lectura: asignar **Reader**
- Control total sobre un grupo de recursos incluyendo asignar roles: asignar **Owner** en ámbito de grupo de recursos
- Restringir a solo redes (VNets, NSGs): asignar **Network Contributor**
- Permitir solo inicio de sesión en VMs como administrador: asignar **Virtual Machine Administrator Login**
- Aplicar mínimo privilegio usando ámbitos reducidos (un grupo de recursos o un recurso) en lugar de toda la suscripción

## Errores Comunes

- Centrarse solo en "el rol" y olvidar que RBAC es el sistema (rol + asignación + ámbito + principal)
- Pensar que Contributor puede asignar roles (solo Owner y User Access Administrator gestionan asignaciones en RBAC)
- Confundir Virtual Machine Contributor con Contributor: en RBAC, el primero no da acceso a red ni storage de las VMs
- Creer que "administrar VMs sin tocar la red" se resuelve con Contributor (Contributor incluye todo; en RBAC hay que usar Virtual Machine Contributor)
- Asumir que Reader en RBAC permite ver datos dentro de Storage o BD (Reader es plano de control; datos suelen requerir roles de datos)
- Confundir Virtual Machine Administrator Login con Virtual Machine Contributor: uno solo login, el otro crear y gestionar VMs
- Pensar que el ámbito en RBAC se "hereda" como copia (cada asignación aplica en su ámbito; los permisos se evalúan por ámbito)
- Usar Owner o Contributor en RBAC cuando basta un rol más limitado (p. ej. Virtual Machine Contributor o Network Contributor)

## Preguntas

1. ¿Azure RBAC es el sistema de autorización que controla el acceso a los recursos mediante asignación de roles a identidades en un ámbito?

2. ¿En RBAC, el rol es un componente que define los permisos, y la asignación de rol vincula ese rol a una identidad (principal) en un ámbito?

3. ¿Para dar permisos a ingenieros para administrar servidores virtuales sin modificar la infraestructura de red, el rol predefinido adecuado en RBAC es Virtual Machine Contributor?

4. ¿Virtual Machine Contributor en RBAC permite crear y gestionar VMs pero no da acceso a la red virtual ni a la cuenta de almacenamiento de las VMs?

5. ¿En RBAC, Contributor permite gestionar todos los recursos pero no asignar roles (solo Owner y User Access Administrator pueden gestionar asignaciones)?

6. ¿User Access Administrator en RBAC permite gestionar el acceso de usuarios a recursos de Azure (asignar y quitar roles)?

7. ¿El ámbito en RBAC puede ser Management Group, Subscription, Resource Group o un recurso concreto?

8. ¿Network Contributor en RBAC permite gestionar redes (VNets, NSGs, etc.) pero no desplegar ni gestionar VMs?
