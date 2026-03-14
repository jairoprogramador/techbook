# Sincronización Delta (Entra Connect)

La sincronización delta es como actualizar solo las páginas que cambiaron en un libro en lugar de reescribir todo el libro. Entra Connect normalmente sincroniza automáticamente cada 30 minutos, pero si necesitas que un cambio aparezca en la nube de inmediato (por ejemplo, RR.HH. creó un nuevo empleado), puedes forzar una sincronización delta: solo busca qué cambió desde la última vez (nuevo usuario, contraseña modificada, correo editado) y sincroniza solo esos cambios. Es rápido y no sobrecarga el servidor porque no revisa todo desde cero.

## Definición

La sincronización delta (incremental) en Microsoft Entra Connect es el modo de sincronización que solo transfiere los cambios ocurridos desde la última sincronización; es el método por defecto y preferido para la sincronización continua; minimiza tráfico de red y tiempo de procesamiento al comparar solo lo que cambió.

Permite:

- Sincronizar solo los cambios (nuevos usuarios, modificaciones de atributos, contraseñas cambiadas, objetos eliminados) desde la última sincronización
- Ejecutarse automáticamente cada 30 minutos por el scheduler por defecto de Entra Connect
- Forzarse manualmente con PowerShell cuando se necesita sincronizar cambios de inmediato sin esperar el ciclo programado
- Ser rápida y eficiente porque solo procesa cambios, no todos los objetos del directorio
- Usarse para el día a día: cuando se crea un nuevo empleado, se modifica un atributo o se cambia una contraseña

## Componentes

**Sincronización delta (Delta sync)** – Modo de sincronización que compara solo los cambios desde la última ejecución; revisa qué objetos fueron modificados, creados o eliminados en AD local y sincroniza solo esos cambios a Entra ID

**Scheduler (programador)** – Componente de Entra Connect que ejecuta sincronizaciones delta automáticamente cada 30 minutos por defecto; se puede modificar el intervalo o deshabilitar

**Comando PowerShell** – `Start-ADSyncSyncCycle -PolicyType Delta` para forzar una sincronización delta manualmente desde PowerShell en el servidor de Entra Connect

**Base de datos de sincronización** – Base de datos local que Entra Connect mantiene con el estado de los objetos sincronizados; la sincronización delta compara el estado actual de AD con esta base de datos para identificar cambios

**Cambios incrementales** – Modificaciones detectadas desde la última sincronización: objetos nuevos, atributos modificados, objetos eliminados, cambios de contraseña (si PHS está habilitado)

**Requisito de 7 días** – Un delta sync debe ocurrir dentro de 7 días desde el último delta sync (o desde una sincronización inicial si fue la última); si pasan más de 7 días, puede ser necesario ejecutar una sincronización inicial

## Funcionalidad

1. El scheduler de Entra Connect ejecuta sincronizaciones delta automáticamente cada 30 minutos (configurable)
2. En cada ciclo delta, Entra Connect importa desde AD local y desde Entra ID solo los objetos que cambiaron desde la última sincronización
3. Compara los cambios con la base de datos de sincronización local para determinar qué necesita sincronizarse
4. Aplica las reglas de sincronización a los objetos modificados y exporta los cambios a Entra ID
5. Si se necesita sincronizar cambios de inmediato (sin esperar el ciclo de 30 minutos), se ejecuta `Start-ADSyncSyncCycle -PolicyType Delta` desde PowerShell en el servidor de Entra Connect
6. La sincronización delta es rápida porque solo procesa cambios, no todos los objetos del directorio
7. Si no se ejecuta un delta sync dentro de 7 días desde el último, puede ser necesario ejecutar una sincronización inicial para reconciliar el estado

## Casos de Uso

- Sincronizar cambios diarios: nuevos usuarios creados en AD local, modificaciones de atributos (correo, teléfono), cambios de contraseña
- Forzar sincronización inmediata cuando RR.HH. necesita que un nuevo empleado aparezca en Entra ID de inmediato
- Mantener sincronización continua sin sobrecargar el servidor ni la red (solo cambios, no todo el directorio)
- Usar como método estándar después de la sincronización inicial; el scheduler ejecuta delta cada 30 minutos automáticamente

## Errores Comunes

- Creer que la sincronización delta se ejecuta solo cuando se fuerza manualmente (el scheduler la ejecuta cada 30 minutos automáticamente)
- Olvidar que si pasan más de 7 días sin delta sync, puede ser necesario ejecutar una sincronización inicial para reconciliar
- Usar sincronización inicial cuando solo se necesita sincronizar cambios recientes (usar delta para cambios incrementales)

## Preguntas

1. ¿La sincronización delta en Entra Connect solo transfiere los cambios ocurridos desde la última sincronización?

2. ¿El scheduler de Entra Connect ejecuta sincronizaciones delta automáticamente cada 30 minutos por defecto?

3. ¿Para forzar una sincronización delta manualmente se usa el comando `Start-ADSyncSyncCycle -PolicyType Delta`?

4. ¿La sincronización delta es rápida y eficiente porque solo procesa cambios y no todos los objetos del directorio?

5. ¿Un delta sync debe ocurrir dentro de 7 días desde el último delta sync para evitar problemas de sincronización?

6. ¿La sincronización delta se usa para el día a día cuando se crean nuevos usuarios, se modifican atributos o se cambian contraseñas?
