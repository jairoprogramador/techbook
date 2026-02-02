# SAS Token (Shared Access Signature)

## Analogía

Un SAS token en Azure es como una llave temporal que abre solo una puerta concreta (un contenedor, un blob o una cuenta de almacenamiento) durante un tiempo limitado y con permisos limitados (solo leer, solo escribir, etc.). No das la llave maestra de la cuenta (la clave de la cuenta); das un token que incluye quién puede hacer qué, hasta cuándo y, opcionalmente, desde qué IP. Si el token se filtra, puedes revocarlo cambiando la política asociada (si usas una política almacenada) o rotando la clave de la cuenta. Es delegación de acceso sin exponer las credenciales completas.

## Definición

Un SAS (Shared Access Signature) es un token que concede acceso limitado a recursos de Azure Storage (blob, archivo, cola, tabla) durante un período y con permisos definidos, sin exponer la clave de la cuenta; puede ser a nivel de servicio (un recurso concreto), de cuenta (toda la cuenta) o por delegación de usuario (basado en Azure AD).

Permite:

- Delegar acceso a datos (plano de datos) de una cuenta de almacenamiento sin compartir la clave de la cuenta
- Limitar permisos (lectura, escritura, eliminación, lista, etc.), tiempo de validez e IP permitida
- Usar políticas de acceso almacenadas para revocar SAS sin rotar la clave de la cuenta
- Diferenciar SAS basado en clave (Service SAS, Account SAS) de SAS por delegación de usuario (Azure AD, más seguro)
- Integrar con RBAC: el SAS por delegación de usuario requiere que quien lo crea tenga rol de datos (p. ej. Storage Blob Data Owner) en el recurso

## Componentes

**SAS URI** – URL del recurso (blob, contenedor, cuenta, etc.) más parámetros de consulta que incluyen permisos, vigencia, firma y opcionalmente IP y protocolo permitidos

**Service SAS** – SAS firmado con la clave de la cuenta que delega acceso a un recurso de un solo servicio (solo Blob, solo File, solo Queue o solo Table); se genera sobre un contenedor, blob, recurso de cola o tabla

**Account SAS** – SAS firmado con la clave de la cuenta que delega acceso a nivel de cuenta de almacenamiento; puede abarcar varios servicios (Blob, File, Queue, Table) y operaciones de nivel de cuenta

**User delegation SAS** – SAS firmado con credenciales de Azure AD (no con la clave de la cuenta); solo soportado para Blob y Data Lake Storage; quien lo crea debe tener rol RBAC de datos (Storage Blob Data Owner, Contributor o Reader); Microsoft lo recomienda por seguridad

**Permisos del SAS** – Conjunto de permisos concedidos (p. ej. r=read, w=write, d=delete, l=list, a=add, c=create, u=update); depende del tipo de recurso (blob, file, queue, table)

**Vigencia (start, expiry)** – Hora de inicio y de expiración del SAS; fuera de ese intervalo el token no es válido

**Stored access policy (política de acceso almacenada)** – Política con nombre creada en el recurso (contenedor, recurso de cola, tabla, recurso de archivos) que define permisos, inicio y expiración; al asociar un SAS a la política, se puede revocar el SAS modificando o eliminando la política sin rotar la clave de la cuenta

**Restricciones opcionales** – IP permitida (signedIp) y protocolo permitido (signedProtocol: solo HTTPS o HTTP y HTTPS) para endurecer el uso del SAS

## Funcionalidad

1. Se elige el tipo de SAS: Service SAS (recurso concreto), Account SAS (cuenta) o User delegation SAS (blob, con Azure AD)
2. Para Service SAS o Account SAS se usa la clave de la cuenta para firmar; para User delegation SAS se usa la identidad de Azure AD (quien crea el SAS debe tener rol de datos en el recurso)
3. Se definen permisos (lectura, escritura, eliminación, lista, etc.), hora de inicio y de expiración; opcionalmente IP y protocolo (solo HTTPS)
4. Opcionalmente se crea o se usa una política de acceso almacenada en el recurso (contenedor, cola, tabla, recurso de archivos) y se asocia el SAS a esa política; así se puede revocar el SAS modificando la política sin rotar la clave
5. Se genera el SAS: la URL del recurso más los parámetros de consulta (permisos, vigencia, firma, etc.)
6. Quien recibe el SAS URI puede acceder al recurso dentro del período y con los permisos definidos sin necesidad de la clave de la cuenta ni de RBAC
7. Para revocar: si el SAS está asociado a una política almacenada, se modifica o elimina la política; si no, hay que rotar la clave de la cuenta (lo que invalida todos los SAS firmados con esa clave)

## Casos de Uso

- Dar a una aplicación o usuario externo acceso temporal solo a un contenedor o blob con permisos limitados (p. ej. solo lectura, 1 hora)
- Compartir un enlace de descarga o subida con expiración sin exponer la clave de la cuenta
- Usar User delegation SAS cuando se quiere auditar quién generó el SAS y no usar la clave de la cuenta
- Asociar SAS a políticas de acceso almacenadas para poder revocar sin rotar la clave de la cuenta
- Restringir el SAS por IP o solo HTTPS para cumplir requisitos de seguridad
- Delegar acceso a nivel de cuenta (Account SAS) para operaciones en varios servicios cuando no se puede usar User delegation SAS (p. ej. Queue, Table, File)

## Errores Comunes

- Confundir SAS con RBAC: el SAS concede acceso al plano de datos (leer/escribir blobs, etc.); RBAC controla el plano de gestión (crear cuenta, obtener claves) y, con roles de datos, quién puede crear User delegation SAS
- Pensar que un SAS asociado a una política almacenada no se puede revocar sin rotar la clave (se revoca modificando o eliminando la política)
- Creer que User delegation SAS está disponible para Queue, Table o Azure Files (solo está soportado para Blob y Data Lake Storage)
- Asumir que el SAS por defecto restringe el protocolo (hay que especificar signedProtocol para forzar solo HTTPS)
- Tratar el SAS como público: quien tiene el token tiene los permisos que concede; si se filtra, hay que revocar (política) o rotar la clave
- Olvidar que sin política almacenada, revocar un SAS implica rotar la clave de la cuenta (lo que invalida todos los SAS y las aplicaciones que usan esa clave)

## Preguntas

1. ¿Un SAS (Shared Access Signature) concede acceso limitado a recursos de Azure Storage sin exponer la clave de la cuenta?

2. ¿La política de acceso almacenada (stored access policy) permite revocar un SAS asociado a ella modificando o eliminando la política, sin rotar la clave de la cuenta?

3. ¿El User delegation SAS está soportado solo para Blob y Data Lake Storage, y requiere que quien lo crea tenga un rol RBAC de datos (p. ej. Storage Blob Data Owner)?

4. ¿Service SAS delega acceso a un recurso de un solo servicio (Blob, File, Queue o Table) y se firma con la clave de la cuenta?

5. ¿Account SAS delega acceso a nivel de cuenta de almacenamiento y puede abarcar varios servicios (Blob, File, Queue, Table)?

6. ¿Sin política de acceso almacenada, para revocar un SAS firmado con la clave de la cuenta hay que rotar la clave (lo que invalida todos los SAS firmados con esa clave)?
