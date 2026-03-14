# Sincronización Delta vs. Inicial (Entra Connect)

Imagina que tienes que copiar un libro completo a otro lugar. La sincronización inicial es como reescribir todo el libro desde cero: borras lo que había antes, comparas cada página y la copias. La sincronización delta es como actualizar solo las páginas que cambiaron: revisas qué páginas se modificaron desde la última vez y solo copias esas. La inicial es lenta pero necesaria cuando cambias las reglas de qué copiar o cuando instalas el servidor por primera vez. La delta es rápida y es la que usas todos los días para mantener todo al día.

## Definición

En Microsoft Entra Connect existen dos modos de sincronización: **Delta (incremental)** que solo sincroniza cambios desde la última ejecución, y **Initial (inicial)** que borra la base de datos de sincronización y vuelve a analizar y sincronizar todos los objetos desde cero comparando cada atributo. La delta es el método estándar para sincronización continua; la inicial se usa en instalación inicial, tras cambios críticos de reglas de filtrado o cuando se necesita reconciliar el estado completo.

Permite:

- Elegir entre sincronización delta (rápida, solo cambios) o inicial (completa, todo desde cero) según la necesidad
- Usar delta para el día a día: nuevos usuarios, cambios de atributos, contraseñas modificadas
- Usar inicial cuando se necesita reconciliar todo el estado: primera instalación, cambio de reglas de filtrado críticas, reconciliación tras problemas
- Forzar cualquiera de las dos con PowerShell: `Start-ADSyncSyncCycle -PolicyType Delta` o `Start-ADSyncSyncCycle -PolicyType Initial`

## Diferencias clave

**Sincronización Delta:**
- Solo busca cambios desde la última sincronización
- Compara el estado actual de AD con la base de datos de sincronización local
- Rápida y eficiente (solo procesa cambios)
- Se ejecuta automáticamente cada 30 minutos por el scheduler
- Comando: `Start-ADSyncSyncCycle -PolicyType Delta`

**Sincronización Inicial:**
- Borra la base de datos de sincronización y vuelve a analizar todo desde cero
- Compara cada atributo de cada objeto sin usar el estado previo
- Lenta pero completa (procesa todos los objetos)
- No se ejecuta automáticamente (solo manualmente o en primera instalación)
- Comando: `Start-ADSyncSyncCycle -PolicyType Initial`

Para detalles completos de cada tipo, ver los documentos **Sincronización Delta** y **Sincronización Inicial**.

## Comparación de funcionalidad

**Sincronización Delta:**
- Importa solo objetos que cambiaron desde la última sincronización
- Compara cambios con la base de datos de sincronización existente
- Aplica reglas solo a objetos modificados
- Rápida: procesa solo cambios

**Sincronización Inicial:**
- Borra la base de datos de sincronización completamente
- Importa todos los objetos (no solo cambios)
- Compara cada atributo de cada objeto desde cero
- Aplica reglas a todos los objetos
- Lenta: procesa todo el directorio

Para el flujo detallado de cada tipo, ver los documentos **Sincronización Delta** y **Sincronización Inicial**.

## Cuándo usar cada una

**Usar Sincronización Delta cuando:**
- Se crea un nuevo usuario en AD local y se necesita que aparezca en Entra ID rápidamente
- Se modifican atributos (correo, teléfono, nombre) y se necesita sincronizar el cambio
- Se cambia una contraseña y PHS está habilitado
- Se necesita sincronizar cambios de forma inmediata sin esperar el ciclo de 30 minutos
- Es el día a día: sincronización continua de cambios incrementales

**Usar Sincronización Inicial cuando:**
- Se instala Entra Connect por primera vez (primera sincronización)
- Se cambian reglas de filtrado críticas (por ejemplo, cambiar qué OUs se sincronizan) y se necesita que la base de datos refleje el nuevo filtro
- Se necesita reconciliar el estado completo tras problemas o inconsistencias
- Han pasado más de 7 días sin sincronización delta y se requiere reconciliación

## Casos de Uso

**Sincronización Delta:**
- RR.HH. crea un nuevo empleado y necesita que aparezca en Entra ID de inmediato → `Start-ADSyncSyncCycle -PolicyType Delta`
- Se modifica el correo de un usuario y se necesita sincronizar el cambio → el scheduler lo sincroniza en el próximo ciclo (30 min) o se fuerza con delta
- Cambios diarios: nuevos usuarios, atributos modificados, contraseñas cambiadas

**Sincronización Inicial:**
- Primera instalación de Entra Connect → se ejecuta inicial para sincronizar todo el directorio
- Se cambia la regla de filtrado para excluir una OU completa → se ejecuta inicial para que la base de datos refleje el nuevo filtro
- Reconciliación completa tras problemas o más de 7 días sin delta sync

## Errores Comunes

- Usar sincronización inicial cuando solo se necesita sincronizar cambios recientes (usar delta para cambios incrementales)
- Confundir cuándo usar cada una: delta para cambios diarios, inicial para reconciliación completa o cambios de configuración críticos
- Ejecutar inicial sin necesidad (es lenta y puede sobrecargar el servidor; usar delta cuando sea posible)
- Olvidar que el scheduler ejecuta delta automáticamente cada 30 minutos (no hace falta forzar delta a menos que se necesite inmediato)
- Creer que inicial se ejecuta automáticamente (solo se ejecuta manualmente o en primera instalación)

## Tips para el examen AZ-104

- **Si la pregunta menciona "cambios", "nuevos usuarios" o "actualización de contraseñas"** → la respuesta casi siempre será **Delta**
- **Si menciona "nueva configuración", "cambio de esquema", "instalación" o "reconciliación completa"** → la respuesta será **Initial**
- **Comando para delta**: `Start-ADSyncSyncCycle -PolicyType Delta`
- **Comando para inicial**: `Start-ADSyncSyncCycle -PolicyType Initial`
- **Scheduler por defecto**: ejecuta delta cada 30 minutos automáticamente
- **Delta es el método estándar** para sincronización continua; inicial es para casos específicos

## Preguntas

1. ¿La diferencia principal entre sincronización delta e inicial es que delta solo busca cambios desde la última sincronización, mientras que inicial borra la base de datos y analiza todo desde cero?

2. ¿Se debe usar sincronización delta cuando se crea un nuevo usuario, se modifican atributos o se cambian contraseñas?

3. ¿Se debe usar sincronización inicial al instalar Entra Connect por primera vez o tras cambiar reglas de filtrado críticas?

4. ¿El comando `Start-ADSyncSyncCycle -PolicyType Delta` fuerza una sincronización incremental y `Start-ADSyncSyncCycle -PolicyType Initial` fuerza una sincronización completa?

5. ¿El scheduler de Entra Connect ejecuta sincronizaciones delta automáticamente cada 30 minutos, pero no ejecuta inicial automáticamente?

6. ¿Si la pregunta del examen menciona "cambios" o "nuevos usuarios" la respuesta suele ser Delta, y si menciona "instalación" o "nueva configuración" suele ser Initial?
