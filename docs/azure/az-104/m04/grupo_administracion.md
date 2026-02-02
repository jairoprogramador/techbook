# Grupo de administración (Azure)

## Analogía

Un grupo de administración en Azure es como el nivel superior de organización de una empresa: por encima de las suscripciones. Imagina que tienes varias suscripciones (una por departamento o por entorno). En lugar de aplicar las mismas políticas y permisos a cada suscripción por separado, creas un grupo de administración que las contiene. Las políticas y los permisos que asignas al grupo se heredan por todas las suscripciones que están dentro. Puedes tener grupos dentro de grupos (hasta 6 niveles) para reflejar la estructura de la organización. No es facturación: es gobernanza jerárquica.

## Definición

Un grupo de administración en Azure es un contenedor jerárquico que agrupa suscripciones (y otros grupos de administración) para aplicar gobernanza de forma centralizada: políticas de Azure Policy, permisos RBAC y estructura organizativa; no es una unidad de facturación.

Permite:

- Agrupar suscripciones bajo un mismo nodo para aplicar políticas y permisos de forma heredada
- Crear jerarquías de hasta 6 niveles (grupo raíz y hasta 5 niveles hijos)
- Asignar políticas de Azure Policy al grupo de administración para que hereden todas las suscripciones hijas
- Asignar roles RBAC al grupo de administración para que los permisos apliquen a todas las suscripciones hijas
- Organizar la estructura de gobernanza sin cambiar la facturación (cada suscripción sigue facturando por separado)

## Componentes

**Grupo raíz (tenant root group)** – Grupo de administración de nivel superior; todas las suscripciones y grupos hijos pertenecen a la jerarquía bajo el raíz

**Jerarquía** – Estructura de grupos de administración; hasta 6 niveles (raíz + 5 niveles); cada grupo puede contener suscripciones y/o grupos hijos

**Suscripciones** – Cada suscripción pertenece a un solo grupo de administración (o al raíz); hereda políticas y permisos del grupo y de sus ancestros

**Herencia de políticas** – Las políticas asignadas a un grupo de administración se aplican a ese grupo y a todos los grupos y suscripciones descendientes

**Herencia de RBAC** – Los roles asignados a un grupo de administración aplican a ese grupo y a todos los grupos y suscripciones descendientes

**Protección del grupo raíz** – El grupo raíz puede tener configuraciones especiales (p. ej. políticas que no pueden excluirse) para garantizar gobernanza en todo el tenant

## Funcionalidad

1. Se crea un grupo de administración en el tenant (o se usa el grupo raíz por defecto)
2. Se mueven suscripciones al grupo de administración (o se crean grupos hijos bajo el raíz u otro grupo)
3. Se asignan políticas de Azure Policy al grupo de administración; las políticas heredan a todas las suscripciones hijas
4. Se asignan roles RBAC al grupo de administración; los permisos heredan a todas las suscripciones hijas
5. Una suscripción puede estar solo en un grupo de administración; al moverla, hereda las políticas y permisos del nuevo grupo
6. La jerarquía permite reflejar la estructura organizativa (p. ej. Producción, Desarrollo, cada uno con sus suscripciones)
7. El grupo de administración no agrupa facturación; cada suscripción sigue facturando por separado; Cost Management puede filtrar por grupo de administración

## Casos de Uso

- Aplicar políticas de cumplimiento (etiquetado, ubicaciones permitidas) a todas las suscripciones de la organización desde un solo punto
- Delegar permisos a nivel de grupo de administración (p. ej. equipo de gobernanza con acceso a todas las suscripciones de Producción)
- Organizar suscripciones por departamento, entorno o región bajo grupos de administración
- Crear jerarquía de gobernanza (raíz → Producción/Desarrollo → suscripciones) sin cambiar la facturación
- Garantizar que ninguna suscripción quede fuera de las políticas asignando al grupo raíz
- Analizar costos por grupo de administración en Cost Management para ver gasto por área

## Errores Comunes

- Confundir grupo de administración con grupo de recursos (el grupo de administración agrupa suscripciones y está por encima; el grupo de recursos agrupa recursos dentro de una suscripción)
- Pensar que el grupo de administración agrupa facturación (cada suscripción factura por separado; el grupo de administración es para gobernanza)
- Creer que una suscripción puede estar en varios grupos de administración (cada suscripción pertenece a un solo grupo de administración)
- Asumir que se pueden tener más de 6 niveles en la jerarquía (máximo 6: raíz + 5 niveles hijos)
- Olvidar que las políticas asignadas al grupo de administración heredan a todas las suscripciones hijas (puede afectar suscripciones que no se esperaba)

## Preguntas

1. ¿Un grupo de administración en Azure agrupa suscripciones (y otros grupos de administración) para aplicar gobernanza de forma jerárquica?

2. ¿Las políticas de Azure Policy asignadas a un grupo de administración heredan a todas las suscripciones contenidas en ese grupo y en sus hijos?

3. ¿Cada suscripción pertenece a un solo grupo de administración (o al grupo raíz)?

4. ¿El grupo de administración es una unidad de facturación o solo de gobernanza (políticas y permisos)?

5. ¿La jerarquía de grupos de administración puede tener hasta 6 niveles (raíz + 5 niveles hijos)?

6. ¿Los roles RBAC asignados a un grupo de administración aplican a todas las suscripciones descendientes?
