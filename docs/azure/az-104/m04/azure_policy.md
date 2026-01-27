# Azure Policy

## Analogía

Azure Policy es como las reglas de una empresa que todos deben seguir, sin importar quién seas o qué cargo tengas. Imagina que trabajas en una oficina donde hay reglas estrictas: todos los documentos deben tener una etiqueta del departamento al que pertenecen, todas las puertas deben estar cerradas con llave, y todos los computadores deben tener un software de seguridad instalado. Estas reglas se aplican automáticamente a todos, desde el empleado nuevo hasta el director. Si alguien intenta crear un documento sin etiqueta, el sistema simplemente no lo permite. Es como tener un supervisor automático que vigila que todo cumpla con las normas de la empresa.

## Definición

Azure Policy es un servicio de gobernanza que aplica reglas y estándares a los recursos de Azure, independientemente de quién los cree o modifique.

Permite:

- Controlar qué se puede hacer en Azure sin importar el usuario o rol
- Aplicar cumplimiento normativo y estándares organizacionales
- Forzar etiquetado y nomenclatura de recursos
- Garantizar seguridad mediante políticas como cifrado de discos
- Estandarizar configuraciones en toda la organización

## Componentes

**Definición de Política** – Regla o conjunto de reglas que definen qué está permitido o no permitido

**Asignación de Política** – Aplicación de una política a un ámbito específico (suscripción, grupo de recursos, etc.)

**Efecto de Política** – Acción que se toma cuando se viola una política (denegar, auditar, modificar)

**Iniciativa** – Grupo de políticas relacionadas que se aplican juntas para cumplir un objetivo

**Cumplimiento** – Estado que indica si los recursos cumplen con las políticas asignadas

## Funcionalidad

1. Se crea o selecciona una definición de política que establece las reglas
2. Se asigna la política a un ámbito específico (suscripción, grupo de recursos, etc.)
3. Azure Policy evalúa los recursos existentes y nuevos contra la política
4. Si un recurso viola la política, se aplica el efecto configurado (denegar, auditar, etc.)
5. Se genera un reporte de cumplimiento mostrando qué recursos cumplen o violan las políticas
6. Las políticas se aplican automáticamente sin importar quién crea o modifica los recursos

## Casos de Uso

- Forzar etiquetado obligatorio de recursos para organización y facturación
- Garantizar que todos los discos estén cifrados para cumplir requisitos de seguridad
- Prevenir la creación de cuentas de almacenamiento con acceso público
- Asegurar que todas las VMs tengan agentes de monitoreo instalados
- Estandarizar nombres y configuraciones de recursos en toda la organización
- Cumplir con requisitos normativos como HIPAA, PCI-DSS o GDPR

## Preguntas

1. ¿Azure Policy controla qué se puede hacer en Azure independientemente de quién sea el usuario o el rol asignado?

2. ¿Azure Policy puede forzar el etiquetado obligatorio de recursos en una organización?

3. ¿Qué efecto de política se aplica cuando un recurso viola una política configurada para denegar?

4. ¿Azure Policy puede garantizar que todos los discos estén cifrados automáticamente?

5. ¿Una iniciativa de Azure Policy agrupa múltiples políticas relacionadas para cumplir un objetivo común?
