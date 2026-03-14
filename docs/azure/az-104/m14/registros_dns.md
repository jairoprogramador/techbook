# Registros DNS (Azure)

## Analogía

Los registros DNS son como las entradas de la guía: a cada nombre (o nombre + tipo) le corresponde una respuesta. "www" con tipo A significa "este nombre va a esta IP"; "mail" con tipo MX significa "el correo de este dominio lo sirve este servidor". En Azure DNS (zona pública o privada) creas conjuntos de registros (record sets): mismo nombre y mismo tipo agrupados, con uno o más valores. Por ejemplo, un registro A para "servidor" con valor 10.0.1.5 hace que servidor.zonadominio.com resuelva a 10.0.1.5. Los tipos más usados son A (IPv4), AAAA (IPv6), CNAME (alias), MX (correo), TXT (texto) y PTR (IP a nombre).

## Definición

Los registros DNS en Azure son las entradas que definen la resolución de nombres dentro de una zona DNS (pública o privada); se organizan en conjuntos de registros (record sets): mismo nombre y mismo tipo en la zona, con uno o más valores; Azure DNS soporta los tipos estándar A, AAAA, CNAME, MX, PTR, SOA, SRV y TXT.

Permite:

- Definir la resolución de un nombre (o nombre + tipo) a una IP, otro nombre, servidor de correo, etc., según el tipo de registro
- Usar los mismos tipos de registros en zonas DNS públicas y privadas
- Agrupar varios valores en un mismo conjunto de registros cuando el estándar lo permite (por ejemplo, varios registros A con el mismo nombre para round-robin básico)
- Crear registros manualmente o, en zonas privadas con registro automático, dejar que Azure cree registros A (y PTR) para las VMs

## Componentes

**Conjunto de registros (record set)** – Colección de registros DNS con el mismo nombre y el mismo tipo dentro de una zona; la mayoría tiene un solo registro; algunos tipos (A, AAAA, etc.) pueden tener varios valores en el mismo conjunto; SOA y CNAME solo pueden tener un registro por conjunto

**Registro A** – Asocia un nombre a una dirección IPv4 (por ejemplo, www → 203.0.113.5); uno de los más usados para resolver nombres a IP

**Registro AAAA** – Asocia un nombre a una dirección IPv6

**Registro CNAME** – Alias: un nombre apunta a otro nombre (por ejemplo, www → contoso.azurewebsites.net); el estándar DNS no permite más de un CNAME por nombre ni CNAME en el vértice de la zona (nombre raíz)

**Registro MX** – Indica los servidores de correo para el dominio (prioridad y nombre del servidor); usado para el enrutamiento del correo electrónico

**Registro PTR** – Resolución inversa: asocia una IP a un nombre; en zonas privadas se usa a menudo para que la IP resuelva al nombre de la VM (reverse lookup)

**Registro SOA** – Registro de inicio de autoridad; hay uno por zona con información del servidor primario, serial, tiempos de refresco, etc.; Azure lo crea automáticamente en la zona

**Registro SRV** – Define servicios por protocolo y puerto (por ejemplo, servicio, prioridad, peso, puerto y destino); usado por algunos protocolos (SIP, XMPP, etc.)

**Registro TXT** – Valor de texto; se usa para SPF, DKIM, verificación de dominio, etc.; puede haber varios valores TXT en el mismo conjunto

**TTL (Time to Live)** – Tiempo en segundos que los resolvers pueden cachear la respuesta; cada conjunto de registros tiene un TTL configurable

## Funcionalidad

1. Dentro de una zona DNS (pública o privada) se crean conjuntos de registros: se elige el nombre (relativo a la zona), el tipo (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT) y el valor o valores
2. Para un registro A se indica la IPv4; para AAAA, la IPv6; para CNAME, el nombre de destino (FQDN); para MX, prioridad y servidor de correo; para TXT, el texto; etc.
3. Se puede configurar el TTL del conjunto de registros
4. En zonas privadas con registro automático, Azure crea y mantiene registros A (y opcionalmente PTR) para las VMs de las VNets enlazadas; el resto de tipos se crean manualmente
5. En zonas públicas todos los registros se crean manualmente (o por automatización externa)
6. Las consultas DNS a ese nombre y tipo devuelven los valores del conjunto de registros según el estándar DNS (por ejemplo, un A devuelve la IP; un CNAME devuelve el nombre al que apunta)
7. SOA existe una vez por zona y Azure lo gestiona; CNAME y SOA solo admiten un registro por conjunto; A, AAAA, MX, TXT, SRV pueden tener varios valores en el mismo conjunto cuando el estándar lo permite

## Casos de Uso

- Crear registros A o AAAA para que un nombre (www, api, servidor) resuelva a una IP en zona pública o privada
- Usar CNAME para apuntar un subdominio a un recurso de Azure (App Service, Storage, etc.) o a otro nombre
- Configurar MX y TXT para el correo del dominio (servidores de correo, SPF, DKIM)
- Usar TXT para verificación de dominio o registros de seguridad
- En zonas privadas, usar registro automático para que las VMs tengan registro A (y PTR) sin crearlos a mano
- Usar PTR en zona privada para resolución inversa (IP → nombre)

## Errores Comunes

- Crear un CNAME en el vértice (apex) de la zona (nombre raíz del dominio); el estándar DNS no lo permite; en Azure se pueden usar registros "alias" para el vértice en algunos escenarios
- Confundir el nombre del registro con el FQDN (en la zona contoso.com, el nombre "www" da el FQDN www.contoso.com; el nombre "@" o vacío suele referirse al vértice)
- Pensar que un conjunto de registros puede mezclar tipos (cada conjunto tiene un solo tipo: A, o CNAME, o MX, etc.)
- Olvidar que SOA y CNAME solo pueden tener un registro por conjunto (no varios valores)
- En zona privada, esperar que el registro automático cree MX, CNAME, etc. (solo crea A y opcionalmente PTR para VMs)

## Preguntas

1. ¿Un conjunto de registros (record set) en Azure DNS agrupa registros con el mismo nombre y el mismo tipo dentro de una zona?

2. ¿El registro A asocia un nombre a una dirección IPv4 y el registro AAAA a una dirección IPv6?

3. ¿El registro CNAME es un alias que apunta un nombre a otro nombre (y no puede haber más de un CNAME por nombre ni CNAME en el vértice de la zona según el estándar)?

4. ¿Los registros MX definen los servidores de correo del dominio (prioridad y nombre del servidor)?

5. ¿En una zona DNS privada con registro automático, Azure crea registros A (y opcionalmente PTR) para las VMs; el resto de tipos se crean manualmente?

6. ¿Azure DNS soporta los tipos de registro estándar A, AAAA, CNAME, MX, PTR, SOA, SRV y TXT tanto en zonas públicas como privadas?
