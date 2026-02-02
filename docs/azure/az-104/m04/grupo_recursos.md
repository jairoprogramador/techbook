# Grupo de recursos (Azure)

## Analogía

Un grupo de recursos en Azure es como una carpeta donde guardas todo lo que pertenece a un proyecto o a una aplicación: la VM, la red, el disco, la cuenta de almacenamiento. La carpeta tiene un nombre y una ubicación (región), pero los recursos que contiene pueden estar en otras regiones. Si borras la carpeta, se borra todo lo que hay dentro. No puedes meter la misma pieza en dos carpetas a la vez: cada recurso está en un solo grupo de recursos. Sirve para organizar, facturar y aplicar permisos o políticas a todo el conjunto.

## Definición

Un grupo de recursos en Azure es un contenedor lógico que agrupa recursos relacionados para una solución o un proyecto; pertenece a una suscripción, tiene un nombre y una ubicación (que solo afecta a dónde se almacenan los metadatos del grupo, no a la ubicación de los recursos que contiene).

Permite:

- Agrupar recursos (VMs, redes, almacenamiento) que comparten ciclo de vida o propósito
- Aplicar RBAC, etiquetas y políticas al grupo de recursos para que hereden los recursos
- Eliminar todos los recursos del grupo de una vez al eliminar el grupo de recursos
- Organizar la facturación y el reporting por grupo de recursos
- Mover recursos entre grupos de recursos de la misma suscripción (según el tipo)

## Componentes

**Nombre del grupo de recursos** – Identificador único del grupo dentro de la suscripción

**Ubicación del grupo de recursos** – Región donde se almacenan los metadatos del grupo; los recursos del grupo pueden estar en otras regiones

**Recursos** – Entidades gestionables (VMs, redes, almacenamiento, etc.) que pertenecen al grupo; cada recurso pertenece a un solo grupo de recursos

**Suscripción** – Contenedor al que pertenece el grupo de recursos; todos los recursos del grupo pertenecen a la misma suscripción

**Etiquetas** – Pares clave-valor aplicados al grupo de recursos; los recursos pueden heredar o tener sus propias etiquetas

**Bloqueos** – Bloqueos a nivel de grupo de recursos protegen todos los recursos del grupo contra eliminación o modificación

## Funcionalidad

1. Se crea un grupo de recursos en una suscripción, con nombre y ubicación (región de metadatos)
2. Se crean o mueven recursos al grupo de recursos; cada recurso pertenece a un solo grupo
3. Los recursos del grupo pueden estar en distintas regiones según el tipo de recurso
4. Se asignan roles RBAC al grupo de recursos para que los identidades hereden permisos sobre todos los recursos del grupo
5. Se aplican etiquetas al grupo de recursos para organización y facturación; las políticas pueden exigir etiquetas
6. Se pueden asignar políticas de Azure Policy al grupo de recursos para evaluar los recursos contenidos
7. Al eliminar el grupo de recursos se eliminan todos los recursos que contiene (salvo bloqueos en recurso o grupo)
8. Se pueden mover recursos entre grupos de recursos de la misma suscripción si el tipo de recurso lo permite

## Casos de Uso

- Agrupar todos los recursos de una aplicación (VM, red, disco, almacenamiento) para gestionarlos como unidad
- Aplicar permisos RBAC al grupo de recursos para que un equipo solo acceda a los recursos de ese proyecto
- Eliminar un entorno completo (p. ej. desarrollo o prueba) eliminando el grupo de recursos
- Organizar facturación y costos por grupo de recursos en Cost Management
- Aplicar políticas o etiquetado obligatorio a nivel de grupo de recursos
- Separar recursos por entorno (prod, staging, dev) usando un grupo de recursos por entorno

## Errores Comunes

- Creer que la ubicación del grupo de recursos determina la ubicación de los recursos (solo define dónde se guardan los metadatos; los recursos pueden estar en otras regiones)
- Pensar que un recurso puede pertenecer a varios grupos de recursos (cada recurso pertenece a un solo grupo)
- Confundir grupo de recursos con grupo de administración (el grupo de recursos está dentro de una suscripción; el grupo de administración está por encima de las suscripciones)
- Asumir que se puede mover un grupo de recursos a otra suscripción (se mueven los recursos a otro grupo; el grupo en sí no se “mueve” de suscripción)
- Olvidar que eliminar el grupo de recursos elimina todos los recursos que contiene (usar bloqueos para proteger grupos críticos)

## Preguntas

1. ¿Un grupo de recursos es un contenedor lógico que agrupa recursos relacionados y pertenece a una suscripción?

2. ¿Cada recurso en Azure pertenece a un solo grupo de recursos?

3. ¿La ubicación del grupo de recursos define solo dónde se almacenan los metadatos y no obliga a los recursos a estar en esa región?

4. ¿Al eliminar un grupo de recursos se eliminan todos los recursos que contiene (salvo bloqueos)?

5. ¿Se pueden asignar roles RBAC al grupo de recursos para que los permisos apliquen a todos los recursos del grupo?

6. ¿Los recursos de un grupo de recursos pueden estar en regiones distintas según el tipo de recurso?
