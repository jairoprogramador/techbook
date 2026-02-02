# Recurso (Azure)

## Analogía

Un recurso en Azure es como una pieza concreta de infraestructura que creas y usas: una máquina virtual, una cuenta de almacenamiento, una red virtual o una base de datos. Cada pieza tiene un tipo, un nombre, una ubicación y pertenece a un grupo de recursos y a una suscripción. No puedes tener un recurso suelto; siempre está dentro de un grupo de recursos y de una suscripción. Es la unidad mínima que Azure Resource Manager gestiona: crear, modificar, eliminar o asignar permisos.

## Definición

Un recurso en Azure es una entidad gestionable que proporciona un servicio de Azure: tiene un tipo (provider/type, p. ej. Microsoft.Compute/virtualMachines), un nombre único dentro de un ámbito, una región (ubicación) y pertenece a un grupo de recursos y a una suscripción.

Permite:

- Representar cada pieza de infraestructura (VM, red, almacenamiento, etc.) como entidad gestionable
- Tener un ciclo de vida independiente: crear, actualizar, eliminar o bloquear
- Recibir asignación de roles RBAC y de etiquetas para control de acceso y organización
- Ser el objetivo de políticas de Azure Policy y de plantillas ARM
- Pertenecer a un solo grupo de recursos y a una sola suscripción en todo momento

## Componentes

**Tipo de recurso** – Identificador que define qué servicio de Azure representa (p. ej. Microsoft.Storage/storageAccounts, Microsoft.Compute/virtualMachines)

**Nombre del recurso** – Identificador del recurso dentro de su grupo de recursos; debe ser único en ese grupo para ese tipo

**Región (ubicación)** – Ubicación geográfica donde se despliega el recurso; no todos los tipos están disponibles en todas las regiones

**Grupo de recursos** – Contenedor al que pertenece el recurso; un recurso pertenece a un solo grupo de recursos

**Suscripción** – Contenedor de facturación y límites; el recurso hereda la suscripción del grupo de recursos

**Identificador del recurso (Resource ID)** – Ruta única que identifica el recurso en Azure (suscripción, grupo de recursos, proveedor, tipo, nombre)

**Etiquetas** – Pares clave-valor opcionales aplicados al recurso para organización y facturación

## Funcionalidad

1. Se crea un recurso en una suscripción y en un grupo de recursos existente (o se crea el grupo al mismo tiempo)
2. Se elige el tipo de recurso, el nombre y la región según el servicio de Azure
3. El recurso recibe un identificador único (Resource ID) que lo identifica en toda la suscripción
4. Se pueden asignar etiquetas al recurso para organización, reporting o políticas
5. Se asignan roles RBAC al recurso (o se heredan del grupo de recursos o la suscripción) para controlar quién puede gestionarlo
6. Las políticas de Azure Policy se evalúan sobre el recurso según el ámbito de asignación
7. Un recurso puede moverse entre grupos de recursos de la misma suscripción (según el tipo); no puede cambiar de suscripción solo (se mueve con el grupo de recursos)
8. Al eliminar el grupo de recursos se eliminan todos los recursos que contiene (salvo bloqueos)

## Casos de Uso

- Crear y gestionar infraestructura (VMs, redes, almacenamiento) como unidades discretas
- Organizar recursos relacionados colocándolos en el mismo grupo de recursos
- Aplicar etiquetas a recursos por proyecto, departamento o entorno para facturación y gobernanza
- Asignar permisos a nivel de recurso cuando no se quiere dar acceso a todo el grupo de recursos
- Bloquear recursos críticos contra eliminación o modificación accidental
- Definir infraestructura como código describiendo recursos en plantillas ARM

## Errores Comunes

- Pensar que un recurso puede existir sin grupo de recursos (todo recurso debe pertenecer a un grupo de recursos)
- Creer que un recurso puede estar en varias suscripciones (pertenece a una sola suscripción a través de su grupo de recursos)
- Confundir el nombre del recurso con el Resource ID (el Resource ID es la ruta completa; el nombre es único solo dentro del grupo)
- Asumir que todos los tipos de recurso pueden moverse entre regiones (la movilidad depende del tipo; muchos no permiten cambio de región)
- Olvidar que eliminar un grupo de recursos elimina todos los recursos que contiene (usar bloqueos para proteger recursos críticos)

## Preguntas

1. ¿Un recurso en Azure debe pertenecer siempre a un grupo de recursos y a una suscripción?

2. ¿El nombre de un recurso debe ser único dentro del grupo de recursos para ese tipo de recurso?

3. ¿El Resource ID identifica de forma única el recurso en Azure (suscripción, grupo de recursos, tipo, nombre)?

4. ¿Un recurso puede pertenecer a más de un grupo de recursos a la vez?

5. ¿Las etiquetas se aplican al recurso para organización y facturación y son opcionales?

6. ¿Al eliminar un grupo de recursos se eliminan todos los recursos que contiene (salvo que tengan bloqueo)?
