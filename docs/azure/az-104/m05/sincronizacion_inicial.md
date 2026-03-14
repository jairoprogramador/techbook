# Sincronización Inicial (Entra Connect)

La sincronización inicial es como reescribir todo un libro desde cero: borras lo que había antes, comparas cada página con el original y la copias. En Entra Connect, la sincronización inicial borra la base de datos de sincronización y vuelve a analizar y sincronizar todos los objetos del directorio desde cero, comparando cada atributo de cada objeto. Es lenta porque procesa todo el directorio, pero es necesaria cuando instalas el servidor por primera vez, cuando cambias reglas de filtrado críticas o cuando necesitas reconciliar el estado completo tras problemas.

## Definición

La sincronización inicial (Initial sync) en Microsoft Entra Connect es el modo de sincronización que borra la base de datos de sincronización local y vuelve a analizar y sincronizar todos los objetos desde cero, comparando cada atributo de cada objeto en AD local con Entra ID; es lenta pero completa y se usa en instalación inicial, tras cambios críticos de reglas de filtrado o cuando se necesita reconciliar el estado completo.

Permite:

- Borrar la base de datos de sincronización y reconstruirla desde cero con el estado completo del directorio
- Comparar cada atributo de cada objeto en AD local con Entra ID para reconciliar diferencias
- Aplicar todas las reglas de sincronización a todos los objetos, no solo a los que cambiaron
- Sincronizar todo el directorio cuando se instala Entra Connect por primera vez
- Reflejar cambios críticos de configuración (por ejemplo, nuevas reglas de filtrado) en toda la base de datos
- Reconciliar el estado completo tras problemas o inconsistencias

## Componentes

**Sincronización inicial (Initial sync)** – Modo de sincronización que borra la base de datos de sincronización y vuelve a analizar todo desde cero; importa todos los objetos (no solo cambios), compara cada atributo y sincroniza todo lo necesario

**Base de datos de sincronización** – Base de datos local que Entra Connect mantiene con el estado de los objetos sincronizados; en sincronización inicial se borra completamente y se reconstruye con el estado completo

**Comando PowerShell** – `Start-ADSyncSyncCycle -PolicyType Initial` para forzar una sincronización inicial manualmente desde PowerShell en el servidor de Entra Connect

**Análisis completo** – Proceso que compara cada atributo de cada objeto en AD local con Entra ID desde cero, sin usar el estado previo de la base de datos

**Reconstrucción de base de datos** – La base de datos de sincronización se borra y se reconstruye con el estado completo tras la sincronización inicial

**No automática** – La sincronización inicial no se ejecuta automáticamente por el scheduler; se ejecuta manualmente o en casos específicos (primera instalación, cambios críticos)

## Funcionalidad

1. Se ejecuta una sincronización inicial manualmente con `Start-ADSyncSyncCycle -PolicyType Initial` o automáticamente en la primera instalación de Entra Connect
2. Entra Connect borra la base de datos de sincronización local completamente
3. Importa todos los objetos desde AD local y desde Entra ID (no solo los que cambiaron)
4. Compara cada atributo de cada objeto desde cero, sin usar el estado previo de la base de datos
5. Aplica todas las reglas de sincronización a todos los objetos para determinar qué necesita sincronizarse
6. Exporta todos los cambios necesarios a Entra ID (creaciones, actualizaciones, eliminaciones según corresponda)
7. Reconstruye la base de datos de sincronización con el estado completo del directorio
8. La sincronización inicial es lenta porque procesa todos los objetos, no solo cambios

## Casos de Uso

- Primera instalación de Entra Connect: sincronizar todo el directorio por primera vez
- Cambio de reglas de filtrado críticas (por ejemplo, cambiar qué OUs se sincronizan) y se necesita que la base de datos refleje el nuevo filtro en todos los objetos
- Reconciliación completa tras problemas o inconsistencias detectadas
- Cuando han pasado más de 7 días sin sincronización delta y se requiere reconciliación del estado
- Cambio de esquema o configuración que afecta cómo se sincronizan los objetos

## Errores Comunes

- Ejecutar sincronización inicial cuando solo se necesita sincronizar cambios recientes (usar sincronización delta para cambios incrementales)
- Creer que la sincronización inicial se ejecuta automáticamente (solo se ejecuta manualmente o en primera instalación; el scheduler ejecuta delta cada 30 minutos)
- Usar inicial sin necesidad (es lenta y puede sobrecargar el servidor; usar delta cuando sea posible)
- Ejecutar inicial tras cambios menores que no requieren reconciliación completa (usar delta para cambios incrementales)

## Preguntas

1. ¿La sincronización inicial en Entra Connect borra la base de datos de sincronización y vuelve a analizar todos los objetos desde cero?

2. ¿La sincronización inicial compara cada atributo de cada objeto en AD local con Entra ID sin usar el estado previo de la base de datos?

3. ¿Para forzar una sincronización inicial manualmente se usa el comando `Start-ADSyncSyncCycle -PolicyType Initial`?

4. ¿La sincronización inicial se usa al instalar Entra Connect por primera vez o tras cambiar reglas de filtrado críticas?

5. ¿La sincronización inicial no se ejecuta automáticamente por el scheduler (solo se ejecuta manualmente o en casos específicos)?

6. ¿La sincronización inicial es más lenta que la delta porque procesa todos los objetos del directorio, no solo cambios?
