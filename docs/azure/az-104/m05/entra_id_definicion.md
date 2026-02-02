# Microsoft Entra ID

Microsoft Entra ID es como el registro central de identidades de tu organización en la nube: quién es cada persona, qué dispositivos son de confianza y a qué aplicaciones puede acceder cada uno. No es el Active Directory que tienes en tu sede; es un directorio en la nube que puede usarse solo (identidades solo en la nube) o conectado al AD local mediante Entra Connect (identidades híbridas). Desde ese registro central se controla el acceso a Azure, Microsoft 365 y muchas aplicaciones con un solo inicio de sesión.

## Definición

Microsoft Entra ID (antes Azure Active Directory) es el servicio de identidad y acceso de Microsoft en la nube: un directorio como servicio (DaaS) que gestiona usuarios, grupos, dispositivos y acceso a aplicaciones y recursos de Azure y Microsoft 365.

Permite:

- Gestionar identidades en la nube (usuarios solo en la nube, sincronizados desde AD local o invitados externos)
- Controlar el acceso a suscripciones de Azure, recursos y aplicaciones mediante integración con RBAC y aplicaciones empresariales
- Ofrecer inicio de sesión único (SSO) para aplicaciones SaaS e integradas con Entra ID
- Asociar un tenant de Entra ID a suscripciones de Azure para que las identidades del directorio autentiquen y reciban permisos
- Diferenciarse de Active Directory Domain Services (AD DS): Entra ID es un directorio en la nube, basado en protocolos web y pensado para la nube; AD DS es un directorio local basado en LDAP/Kerberos

## Componentes

**Tenant (directorio)** – Instancia dedicada de Entra ID asociada a una organización; contiene usuarios, grupos, aplicaciones y configuraciones; cada suscripción de Azure está asociada a un tenant

**Usuario solo en la nube (cloud-only)** – Usuario creado directamente en Entra ID; no existe en un AD local; se administra solo en la nube

**Usuario sincronizado (directory-synced)** – Usuario que proviene de AD local mediante Microsoft Entra Connect; el origen de autoridad es el directorio local

**Usuario invitado (guest)** – Usuario externo invitado al tenant para acceder a recursos o aplicaciones; inicia sesión con su propia identidad (otro tenant, cuenta Microsoft, etc.)

**Grupos** – Colecciones de usuarios, dispositivos o entidades de servicio para asignar permisos o acceso; en Entra ID existen grupos de seguridad y grupos de Microsoft 365

**Ediciones (Free, Premium P1, Premium P2)** – Niveles de funcionalidad: Free (básico); P1 (acceso condicional, SSPR para la nube, writeback de SSPR con Connect, etc.); P2 (Identity Protection, PIM, etc.)

## Funcionalidad

1. Un tenant de Entra ID se crea al registrar una organización en servicios de Microsoft (Azure, Microsoft 365) o de forma explícita
2. Las suscripciones de Azure se asocian a un tenant; las identidades del tenant pueden recibir roles RBAC en la suscripción
3. Se crean o sincronizan usuarios: solo en la nube (creados en Entra ID), sincronizados (desde AD con Entra Connect) o invitados (externos)
4. Se crean grupos (seguridad o Microsoft 365) y se asignan miembros para gestionar acceso a recursos y aplicaciones
5. Se configuran aplicaciones empresariales y SSO para que los usuarios accedan a aplicaciones con una sola identidad
6. Con ediciones Premium se habilitan funciones como Conditional Access, SSPR en la nube, writeback de SSPR con Connect, PIM o Identity Protection
7. Entra ID no reemplaza AD DS en local; puede coexistir con AD DS y sincronizarse mediante Entra Connect (identidad híbrida)

## Casos de Uso

- Gestionar identidades para acceso a Azure y Microsoft 365 desde un único directorio en la nube
- Unificar acceso a aplicaciones SaaS e internas con inicio de sesión único
- Sincronizar usuarios y grupos desde AD local con Entra Connect para identidad híbrida
- Invitar usuarios externos (B2B) para acceder a recursos o aplicaciones sin crear cuentas locales
- Asociar suscripciones de Azure a un tenant para controlar quién administra recursos (RBAC)
- Usar ediciones Premium para políticas de acceso condicional, SSPR o PIM según requisitos de seguridad

## Errores Comunes

- Confundir Entra ID con Active Directory Domain Services (AD DS): Entra ID es un directorio en la nube; AD DS es un directorio local; pueden coexistir y sincronizarse con Entra Connect
- Pensar que una suscripción de Azure puede estar asociada a varios tenants (cada suscripción está asociada a un solo tenant de Entra ID)
- Creer que los usuarios sincronizados se crean o editan principalmente en Entra ID (el origen de autoridad es el AD local; los cambios importantes se hacen en AD y se sincronizan)
- Asumir que todas las funciones (Conditional Access, writeback de SSPR, PIM) están en la edición Free (muchas requieren Premium P1 o P2)
- Usar Entra ID como reemplazo directo de AD DS para unirse a dominios de máquinas locales (Entra ID no es un controlador de dominio; para unión a dominio local se usa AD DS)

## Preguntas

1. ¿Microsoft Entra ID es el servicio de identidad y acceso en la nube que gestiona usuarios, grupos y acceso a aplicaciones y recursos de Azure?

2. ¿Un tenant de Entra ID es la instancia del directorio asociada a una organización y a la que se vinculan suscripciones de Azure?

3. ¿Los usuarios en Entra ID pueden ser solo en la nube, sincronizados desde AD local (con Entra Connect) o invitados externos?

4. ¿Entra ID y Active Directory Domain Services (AD DS) son distintos: Entra ID en la nube, AD DS local, pudiendo coexistir con Entra Connect?

5. ¿Funciones como Conditional Access o writeback de SSPR requieren ediciones Premium de Entra ID y no están en la edición Free?

6. ¿Cada suscripción de Azure está asociada a un solo tenant de Entra ID?
