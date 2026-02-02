# Microsoft Entra Connect

Microsoft Entra Connect es como el puente que une el directorio de empleados de tu sede (Active Directory local) con el directorio en la nube (Entra ID). Sin el puente, tendrías dos listas separadas: una en la oficina y otra en la nube. Con Entra Connect, los usuarios, grupos y otros objetos se copian de forma controlada desde el servidor local hacia Entra ID, de modo que una misma identidad sirve para iniciar sesión en la red local y en Azure. No es Entra ID en sí; es la herramienta que instalas en un servidor local para mantener ambos directorios alineados. Opcionalmente, algunos cambios (como contraseñas restablecidas en la nube) pueden devolverse al directorio local.

## Definición

Microsoft Entra Connect es la herramienta de Microsoft que se instala en un entorno local y sincroniza identidades desde Active Directory Domain Services (AD DS) hacia Microsoft Entra ID, permitiendo identidad híbrida: un mismo usuario existe en el directorio local y en la nube con el mismo origen de autoridad (local).

Permite:

- Sincronizar usuarios, grupos y contactos desde AD DS local hacia Entra ID
- Mantener un único origen de autoridad (normalmente el directorio local) para identidades híbridas
- Opcionalmente sincronizar hashes de contraseña para que el usuario use la misma contraseña en la nube (inicio de sesión unificado)
- Opcionalmente devolver cambios de contraseña desde Entra ID al AD local (writeback de SSPR)
- Filtrar qué objetos se sincronizan (por OU, grupo, atributo) mediante reglas de sincronización
- Usar un servidor en modo staging para probar la sincronización sin exportar a Entra ID

## Componentes

**Motor de sincronización** – Componente que ejecuta importación desde AD y desde Entra ID, aplica reglas de sincronización y exporta cambios a Entra ID

**Reglas de sincronización** – Reglas que definen qué objetos y atributos fluyen desde AD local hacia Entra ID (y opcionalmente en sentido inverso para writeback)

**Password Hash Synchronization (PHS)** – Sincronización de hashes de contraseña desde AD local a Entra ID; el usuario usa la misma contraseña para iniciar sesión en la nube

**Writeback de contraseña** – Devolución de cambios de contraseña (p. ej. SSPR en Entra ID) al AD local; requiere Entra ID Premium y configuración en Connect

**SSPR (Self-Service Password Reset)** – Autoservicio de restablecimiento de contraseña: función de Entra ID que permite a los usuarios cambiar o restablecer su contraseña sin intervención del soporte (p. ej. desde la pantalla de inicio de sesión); con writeback habilitado en Connect, el cambio se escribe de vuelta en el AD local

**Modo staging** – Modo del servidor de Entra Connect en el que se importa y sincroniza pero no se exporta a Entra ID; útil para pruebas o recuperación; en staging no se ejecutan PHS ni writeback

**Usuario sincronizado (directory-synced)** – Usuario en Entra ID cuyo origen es el AD local; se identifica por el atributo sourceAnchor (immutableId); la administración de atributos clave suele hacerse en AD local

**Conector** – Representación de un directorio (AD local o Entra ID) en el motor de sincronización; cada ejecución importa desde los conectores, aplica reglas y exporta a los conectores destino

## Funcionalidad

1. Se instala Microsoft Entra Connect en un servidor unido al dominio, con conectividad a AD DS local y a Entra ID
2. Durante la instalación se configura el bosque AD de origen, las credenciales y la opción de sincronización (express o personalizada)
3. Se elige si se habilita sincronización de hashes de contraseña (PHS) y, si aplica, writeback de contraseña (SSPR writeback)
4. Opcionalmente se configuran filtros (por OU, grupo o atributo) para limitar qué objetos se sincronizan
5. El motor de sincronización ejecuta ciclos periódicos: importa desde AD y desde Entra ID, aplica reglas de sincronización y exporta cambios a Entra ID
6. Los usuarios y grupos sincronizados aparecen en Entra ID como "Synced from on-premises directory" (origen: Windows Server AD)
7. Con PHS, los usuarios pueden iniciar sesión en Entra ID con la misma contraseña que en local
8. Con writeback habilitado, un cambio de contraseña en Entra ID (p. ej. SSPR) se escribe de vuelta en AD local
9. Un servidor en modo staging ejecuta importación y sincronización pero no exporta; no ejecuta PHS ni writeback hasta salir de staging

## Casos de Uso

- Unificar identidades entre AD local y Azure para que los empleados usen una sola cuenta (híbrida)
- Permitir inicio de sesión en Microsoft 365 y aplicaciones integradas con Entra ID usando la contraseña del AD local (con PHS)
- Habilitar autoservicio de restablecimiento de contraseña en la nube y que el cambio se refleje en local (writeback)
- Filtrar la sincronización para que solo ciertas OUs o grupos se repliquen a Entra ID
- Usar un servidor en modo staging para validar reglas o como respaldo antes de promoverlo a activo
- Mantener el AD local como origen de autoridad para usuarios y grupos mientras se usan servicios en la nube

## Errores Comunes

- Confundir Entra Connect con Entra ID (Connect es la herramienta de sincronización que se instala en local; Entra ID es el directorio en la nube)
- Pensar que los usuarios sincronizados se administran solo en Entra ID (los atributos principales suelen administrarse en AD local y se sincronizan a la nube)
- Creer que en modo staging se sincronizan contraseñas o writeback (en staging no hay exportación; PHS y writeback no se ejecutan)
- Asumir que writeback de contraseña funciona sin una edición Premium de Entra ID (se requiere licencia Premium para SSPR writeback)
- Instalar Connect en un controlador de dominio (se recomienda un servidor miembro con acceso al bosque AD)
- Olvidar que solo puede haber un servidor de Entra Connect activo exportando a un mismo tenant (el segundo debe estar en staging o en otro rol)

## Preguntas

1. ¿Microsoft Entra Connect sincroniza identidades desde Active Directory local hacia Microsoft Entra ID?

2. ¿Un usuario "sincronizado desde el directorio local" en Entra ID tiene su origen de autoridad en el AD local?

3. ¿En modo staging el servidor de Entra Connect importa y sincroniza pero no exporta a Entra ID ni ejecuta PHS ni writeback?

4. ¿Password Hash Synchronization permite que el usuario use la misma contraseña para iniciar sesión en la nube que en el AD local?

5. ¿El writeback de contraseña devuelve cambios de contraseña desde Entra ID (p. ej. SSPR) al AD local?

6. ¿Se puede filtrar qué objetos de AD se sincronizan a Entra ID (por OU, grupo o atributo)?
