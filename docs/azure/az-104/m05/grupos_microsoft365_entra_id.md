# Grupos de Microsoft 365 en Entra ID

## Analogía

Un grupo de Microsoft 365 es como un equipo de trabajo completo con dos funciones: por un lado, es un espacio de colaboración donde todos comparten archivos, se comunican y trabajan juntos (como un equipo de Microsoft Teams o un sitio de SharePoint). Por otro lado, es también una identidad que determina quién tiene acceso a qué recursos (como un pase de acceso). Y además, tiene un temporizador incorporado: cuando el proyecto termina, el sistema te avisa y puedes renovarlo si sigue siendo necesario, o se elimina automáticamente si ya no se usa. Es un objeto híbrido que combina colaboración e identidad en una sola entidad, con la ventaja adicional de políticas de expiración automática.

## Definición

Un grupo de Microsoft 365 en Entra ID es un tipo de grupo que funciona como objeto híbrido de colaboración e identidad, proporcionando oportunidades de colaboración mediante acceso a servicios de Microsoft 365 (Teams, SharePoint, Exchange) y recursos de Azure, con la capacidad distintiva de configurar políticas de expiración automática. Solo usuarios pueden ser miembros del grupo, incluyendo personas fuera de la organización.

Permite:

- Proporcionar oportunidades de colaboración mediante espacios de trabajo compartidos
- Funcionar como objeto de colaboración proporcionando acceso a Teams, SharePoint y Exchange
- Actuar como objeto de identidad para administrar acceso a recursos de Azure y aplicaciones
- Incluir solo usuarios como miembros (no dispositivos ni entidades de servicio)
- Permitir que personas fuera de la organización sean miembros del grupo
- Configurar políticas de expiración automática como característica distintiva del tipo de grupo
- Renovar grupos que siguen siendo necesarios antes de su expiración
- Eliminar automáticamente grupos obsoletos que no se renuevan
- Mantener la organización limpia sin gestión manual constante
- Notificar a propietarios antes de la expiración para renovación

## Componentes

**Objeto de Colaboración** – Funcionalidad que proporciona espacios de trabajo compartidos (Teams, SharePoint, correo)

**Objeto de Identidad** – Funcionalidad que gestiona acceso y permisos a recursos de Azure y aplicaciones

**Política de Expiración** – Configuración que define cuándo expira el grupo (ej: 180 días, 1 año)

**Período de Renovación** – Ventana de tiempo antes de la expiración donde se puede renovar el grupo

**Notificaciones** – Alertas enviadas a propietarios antes de la expiración

**Renovación Automática** – Proceso que extiende la vida del grupo si se sigue usando activamente

**Eliminación Automática** – Proceso que elimina el grupo si no se renueva antes de la expiración

**Miembros** – Solo usuarios pueden ser miembros del grupo, incluyendo usuarios de la organización y personas externas

**Propietarios del Grupo** – Usuarios o entidades de servicio responsables de renovar o eliminar el grupo

**Miembros Externos** – Personas fuera de la organización que pueden ser invitadas como miembros del grupo

## Funcionalidad

1. Se crea un grupo de Microsoft 365 en Entra ID con una política de expiración configurada
2. Se agregan usuarios como miembros del grupo (solo usuarios, no dispositivos ni entidades de servicio)
3. Se pueden invitar personas fuera de la organización como miembros del grupo
4. El grupo funciona normalmente para colaboración, comunicación y acceso a recursos
5. Los propietarios (usuarios o entidades de servicio) administran la membresía y configuración del grupo
6. Antes de la fecha de expiración, se envían notificaciones a los propietarios del grupo
7. Los propietarios pueden renovar el grupo si sigue siendo necesario
8. Si el grupo se renueva, se extiende su período de vida según la política
9. Si el grupo no se renueva antes de la expiración, se elimina automáticamente
10. Los recursos y permisos asociados al grupo se eliminan junto con el grupo

## Casos de Uso

- Crear equipos de colaboración con acceso automático a recursos compartidos
- Facilitar colaboración con personas externas a la organización en proyectos compartidos
- Gestionar grupos temporales de proyectos que combinan colaboración e identidad
- Proporcionar acceso a aplicaciones y recursos mientras se facilita la colaboración
- Incluir solo usuarios (internos y externos) en grupos de colaboración
- Mantener la organización limpia eliminando grupos obsoletos automáticamente
- Reducir la sobrecarga administrativa de limpieza manual de grupos
- Aplicar políticas de ciclo de vida a grupos que sirven tanto para colaboración como identidad
- Notificar a propietarios sobre grupos que pueden necesitar renovación
- Cumplir con políticas de gobernanza que requieren revisión periódica de grupos

## Preguntas

1. ¿Un grupo de Microsoft 365 es un objeto híbrido que proporciona oportunidades de colaboración e identidad?

2. ¿Solo usuarios pueden ser miembros de un grupo de Microsoft 365, a diferencia de los grupos de seguridad?

3. ¿Las personas fuera de la organización pueden ser miembros de un grupo de Microsoft 365?

4. ¿Tanto usuarios como entidades de servicio pueden ser propietarios de un grupo de Microsoft 365?

5. ¿Un grupo de Microsoft 365 permite configurar políticas de expiración automática además de sus funciones de colaboración e identidad?
