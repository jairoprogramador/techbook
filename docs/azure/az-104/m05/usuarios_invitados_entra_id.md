# Usuarios invitados

Un usuario invitado en Entra ID es como dar acceso a un colaborador externo sin crearle una cuenta en tu empresa. Imagina que un proveedor o un consultor necesita entrar a tu sitio de SharePoint o a una aplicación que usa Entra ID. En lugar de crearle un usuario interno, lo invitas por correo: él sigue usando su propia identidad (su empresa o su cuenta personal) y tú decides a qué recursos o aplicaciones puede acceder. Entra ID lo reconoce como invitado en tu tenant y aplica las políticas que definas (acceso, Conditional Access, etc.) sin gestionar su contraseña ni su directorio de origen.

## Definición

Un usuario invitado en Microsoft Entra ID es una identidad externa invitada al tenant para acceder a recursos, aplicaciones o grupos; inicia sesión con su propia identidad (otro tenant de Entra ID, cuenta Microsoft u otro proveedor de identidad) y aparece en el directorio como tipo "Guest" (B2B collaboration).

Permite:

- Invitar a personas externas (otra organización, cuenta Microsoft) sin crear cuentas locales ni sincronizar directorios
- Dar acceso a aplicaciones, sitios (SharePoint, Teams) o recursos de Azure asignando al invitado o a grupos que contengan invitados
- Mantener el origen de autoridad en el directorio del invitado; la organización que invita no gestiona su contraseña
- Aplicar políticas de acceso (Conditional Access, MFA) a los invitados como a usuarios internos
- Incluir invitados en grupos de Microsoft 365 o de seguridad para asignar permisos de forma centralizada

## Componentes

**Invitación (B2B)** – Proceso de invitar a un usuario externo por correo; el invitado recibe un enlace y puede canjear la invitación con su identidad existente

**Usuario tipo Guest** – Objeto de usuario en el tenant con origen externo (User type = Guest); el atributo mail o el UPN reflejan la identidad externa

**Origen de identidad** – Directorio o proveedor del invitado (otro tenant de Entra ID, cuenta Microsoft, Google, etc.); la autenticación la realiza el proveedor del invitado

**Acceso a recursos** – Asignación del invitado (o de un grupo que lo contiene) a aplicaciones empresariales, sitios o roles RBAC en Azure

**Políticas de colaboración B2B** – Configuración del tenant que define quién puede invitar invitados, si pueden unirse a grupos, etc.

**Cross-tenant access settings** – Configuración que controla qué usuarios externos de otros tenants pueden acceder a recursos del tenant y bajo qué condiciones

## Funcionalidad

1. Un administrador o usuario con permiso para invitar invitados envía una invitación por correo (o se usa la API de invitación B2B)
2. El invitado recibe el enlace, hace clic y inicia sesión con su identidad (su tenant, cuenta Microsoft u otro IdP)
3. Se crea un objeto de usuario tipo Guest en el tenant; el invitado aparece en el directorio como usuario externo
4. Se asigna al invitado acceso a aplicaciones empresariales, grupos o recursos de Azure (p. ej. mediante grupos de seguridad o de Microsoft 365)
5. El invitado accede a los recursos asignados iniciando sesión con su propia identidad; la organización que invita no gestiona su contraseña
6. Se pueden aplicar políticas de Conditional Access y MFA a los invitados para reforzar la seguridad
7. Las políticas de colaboración B2B y cross-tenant access definen quién puede invitar y qué tenants externos pueden acceder

## Casos de Uso

- Colaborar con proveedores o socios dando acceso a aplicaciones o sitios sin crear cuentas internas
- Incluir consultores o contratistas en equipos de Microsoft 365 (Teams, SharePoint) como invitados
- Asignar acceso a recursos de Azure (p. ej. mediante RBAC) a usuarios externos mediante invitación B2B
- Usar grupos (seguridad o Microsoft 365) que incluyan invitados para centralizar la asignación de acceso
- Aplicar Conditional Access o MFA a invitados para cumplir requisitos de seguridad
- Mantener el origen de autoridad en la organización del invitado sin sincronizar directorios

## Errores Comunes

- Confundir usuario invitado (Guest) con usuario sincronizado (directory-synced): el invitado es externo e inicia sesión con su identidad; el sincronizado proviene del AD local mediante Entra Connect
- Pensar que la organización que invita gestiona la contraseña del invitado (la autenticación la realiza el directorio o IdP del invitado)
- Creer que los invitados no pueden ser miembros de grupos (pueden serlo de grupos de seguridad y de Microsoft 365, según configuración)
- Asumir que B2B no requiere licencias (el acceso a aplicaciones Microsoft 365 por invitados puede requerir licencias o derechos según el recurso)
- Ignorar cross-tenant access o políticas de colaboración B2B al restringir o auditar quién puede invitar y qué tenants pueden acceder

## Preguntas

1. ¿Un usuario invitado (Guest) en Entra ID es una identidad externa invitada al tenant que inicia sesión con su propia identidad?

2. ¿La organización que invita no gestiona la contraseña del invitado porque la autenticación la realiza el directorio o IdP del invitado?

3. ¿Los invitados pueden ser miembros de grupos de seguridad o de Microsoft 365 para asignarles acceso a recursos o aplicaciones?

4. ¿La invitación B2B permite dar acceso a aplicaciones o recursos sin crear un usuario interno ni sincronizar el directorio del invitado?

5. ¿Se pueden aplicar políticas de Conditional Access o MFA a los usuarios invitados en el tenant?

6. ¿El tipo de usuario "Guest" en Entra ID corresponde a colaboración B2B (acceso con identidad externa)?
