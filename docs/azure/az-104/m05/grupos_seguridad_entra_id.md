# Grupos de Seguridad en Entra ID

Un grupo de seguridad en Entra ID es como tener un pase de acceso que determina a qué áreas puedes entrar en un edificio. Imagina que trabajas en una empresa grande con diferentes departamentos: desarrollo, finanzas, recursos humanos, etc. En lugar de dar permisos individuales a cada persona, dispositivo o sistema para cada recurso, creas grupos como "Desarrolladores", "Contadores" o "Gerentes". Puedes incluso tener grupos dentro de grupos: por ejemplo, el grupo "Equipo de Desarrollo" puede contener los grupos "Desarrolladores Senior" y "Desarrolladores Junior". Cuando alguien necesita acceso a un servidor, una base de datos o un sitio web, simplemente lo agregas al grupo correspondiente y automáticamente obtiene todos los permisos de ese grupo. Es como tener llaves maestras organizadas por función: si eres parte del grupo "Desarrolladores", tienes acceso a los servidores de desarrollo, pero no a los de producción. Si cambias de departamento, solo te mueven de grupo y tus permisos se actualizan automáticamente.

## Definición

Un grupo de seguridad en Entra ID es una colección de usuarios, dispositivos, entidades de servicio o grupos que se utiliza para administrar el acceso a recursos compartidos de Azure mediante la asignación de permisos al grupo en lugar de entidades individuales.

Permite:

- Administrar acceso a recursos compartidos de Azure de forma centralizada
- Incluir usuarios, dispositivos, entidades de servicio y grupos como miembros
- Crear grupos anidados donde grupos pueden ser miembros de otros grupos
- Controlar acceso a redes y subredes específicas
- Gestionar permisos en sitios y aplicaciones
- Simplificar la administración asignando permisos al grupo
- Actualizar permisos agregando o removiendo miembros del grupo
- Aplicar políticas de acceso basadas en roles y funciones

## Componentes

**Miembros** – Usuarios, dispositivos, entidades de servicio o grupos que pertenecen al grupo de seguridad

**Grupos Anidados** – Grupos que son miembros de otros grupos, permitiendo jerarquías de membresía

**Permisos Asignados** – Accesos y derechos otorgados al grupo de seguridad

**Recursos Protegidos** – Recursos de Azure, redes o sitios a los que el grupo tiene acceso

**Propietarios** – Usuarios o entidades de servicio que pueden administrar la membresía del grupo

## Funcionalidad

1. Se crea un grupo de seguridad en Entra ID con un nombre descriptivo
2. Se agregan usuarios, dispositivos, entidades de servicio o grupos como miembros del grupo de seguridad
3. Los grupos pueden ser miembros de otros grupos, creando grupos anidados con jerarquías de membresía
4. Se asignan permisos o roles al grupo de seguridad en recursos específicos
5. Los miembros del grupo heredan automáticamente los permisos asignados al grupo
6. Cuando se agrega un nuevo miembro al grupo, obtiene acceso inmediatamente
7. Cuando se remueve un miembro del grupo, pierde el acceso automáticamente
8. Los permisos se pueden asignar a nivel de recurso, red, sitio o aplicación
9. Los propietarios (usuarios o entidades de servicio) pueden administrar la membresía del grupo

## Casos de Uso

- Administrar acceso a máquinas virtuales agrupando usuarios por función (desarrolladores, administradores)
- Controlar acceso a redes virtuales permitiendo solo a grupos específicos
- Gestionar permisos en sitios de SharePoint o aplicaciones empresariales
- Simplificar administración de acceso en recursos de Azure mediante grupos
- Implementar control de acceso basado en roles (RBAC) usando grupos
- Facilitar cambios organizacionales moviendo usuarios entre grupos

## Preguntas

1. ¿Un grupo de seguridad en Entra ID se utiliza para administrar acceso a recursos compartidos?

2. ¿Los miembros de un grupo de seguridad pueden incluir usuarios, dispositivos y entidades de servicio?

3. ¿Un grupo de seguridad puede contener otros grupos como miembros, creando grupos anidados?

4. ¿Los permisos se asignan al grupo de seguridad y todos los miembros heredan esos permisos automáticamente?

5. ¿Tanto usuarios como entidades de servicio pueden ser propietarios de un grupo de seguridad?
