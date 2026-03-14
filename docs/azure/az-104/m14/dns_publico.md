# DNS público (Azure DNS)

## Analogía

DNS público en Azure es como hospedar la guía telefónica de tu dominio en Azure: cuando alguien en Internet busca www.tudominio.com o api.tudominio.com, los servidores DNS de Azure responden con la IP (o el registro que tengas configurado). Tú creas una zona DNS pública para tu dominio (por ejemplo, tudominio.com), añades registros (A, CNAME, MX, etc.) y delegas el dominio desde tu registrador para que apunte a los servidores de nombres de Azure. Azure se convierte en el servidor DNS autoritativo de ese dominio para todo Internet.

## Definición

Azure DNS es el servicio de Azure que permite hospedar zonas DNS públicas (y privadas); una zona DNS pública es autoritativa para un dominio en Internet: los registros que creas (A, AAAA, CNAME, MX, etc.) son los que se devuelven cuando se consulta ese dominio desde cualquier lugar; el dominio debe delegarse desde el registrador a los servidores de nombres de Azure.

Permite:

- Crear zonas DNS públicas para dominios que posees o controlas (por ejemplo, contoso.com)
- Añadir y gestionar registros DNS (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT) que se resuelven en Internet
- Delegar el dominio desde el registrador (donde compraste el dominio) a los servidores de nombres (name servers) que Azure asigna a la zona
- Usar Azure DNS como servidor DNS autoritativo para el dominio: las consultas desde Internet obtienen las respuestas definidas en los registros de la zona
- Integrar con otros servicios de Azure (por ejemplo, App Service, Load Balancer, Traffic Manager) usando registros A, CNAME o alias
- Alojar varias zonas (varios dominios) en la misma suscripción

## Componentes

**Zona DNS (pública)** – Recurso de Azure que representa una zona DNS pública para un dominio; tiene un nombre único globalmente (por ejemplo, contoso.com); contiene los registros DNS del dominio

**Servidores de nombres (name servers)** – Azure asigna un conjunto de servidores de nombres a cada zona (por ejemplo, ns1-01.azure-dns.com, ns2-01.azure-dns.net); el registrador del dominio debe configurar la delegación para que apunte a estos servidores

**Delegación** – Configuración en el registrador del dominio (donde se compró el dominio) que indica que los servidores de nombres autoritativos para el dominio son los de Azure; sin delegación, las consultas no llegarán a Azure DNS

**Registros** – Entradas en la zona (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT) que definen la resolución del dominio; se crean manualmente en la zona

**Autoritativo** – Azure DNS es el servidor autoritativo para la zona: responde con los registros que tú defines; no hace resolución recursiva para otros dominios

**Registrador** – Entidad donde se registró el dominio (por ejemplo, GoDaddy, Namecheap); en el registrador se configura la delegación hacia los name servers de Azure

## Funcionalidad

1. Se crea una zona DNS pública en Azure para el dominio (por ejemplo, contoso.com); Azure asigna servidores de nombres a la zona
2. En el registrador del dominio se configura la delegación: se sustituyen los name servers anteriores por los que Azure muestra para la zona (ns1-xx.azure-dns.com, etc.)
3. Se crean registros en la zona (A, AAAA, CNAME, MX, TXT, etc.) según lo que se quiera exponer (web, correo, API, etc.)
4. Las consultas DNS desde Internet al dominio (o subdominios) llegan a los servidores de Azure y Azure responde con los registros definidos en la zona
5. Se pueden usar registros CNAME o alias para apuntar a recursos de Azure (App Service, Load Balancer, Traffic Manager) sin crear registros A manualmente en algunos escenarios
6. La zona es autoritativa solo para ese dominio; Azure DNS no resuelve otros dominios (no es un resolver recursivo público para dominios arbitrarios)

## Casos de Uso

- Hospedar el DNS del dominio corporativo en Azure para control centralizado y alta disponibilidad
- Apuntar el dominio o subdominios a App Service, Load Balancer, Traffic Manager o otros recursos de Azure mediante registros A, CNAME o alias
- Gestionar registros MX, TXT (SPF, DKIM, etc.) para correo electrónico del dominio
- Tener un único lugar (Azure) para gestionar DNS y recursos en la nube
- Delegar subdominios a otras zonas o servicios si se requiere

## Errores Comunes

- Creer que con solo crear la zona en Azure el dominio ya usa Azure DNS (hay que delegar el dominio en el registrador a los name servers de Azure)
- Confundir zona DNS pública con zona DNS privada (la pública es autoritativa en Internet; la privada solo se resuelve desde VNets enlazadas)
- No actualizar los name servers en el registrador (las consultas seguirán yendo al DNS anterior)
- Pensar que Azure DNS es un resolver recursivo para cualquier dominio (Azure DNS solo responde por las zonas que tú creas; es autoritativo, no recursivo)
- Crear registros con nombres o valores incorrectos (por ejemplo, CNAME en el vértice del dominio tiene limitaciones en el estándar DNS)

## Preguntas

1. ¿Una zona DNS pública de Azure es autoritativa para un dominio y los registros que creas se devuelven cuando se consulta ese dominio desde Internet?

2. ¿Para que el dominio use Azure DNS hay que configurar la delegación en el registrador del dominio para que apunte a los servidores de nombres (name servers) que Azure asigna a la zona?

3. ¿Azure DNS asigna servidores de nombres a cada zona y el registrador debe usar esos name servers para la delegación?

4. ¿Azure DNS en modo zona pública no resuelve dominios que no estén en zonas que tú creas (es autoritativo, no un resolver recursivo público)?

5. ¿Se pueden crear en la zona pública los mismos tipos de registros que en una zona privada (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT)?

6. ¿La zona DNS pública tiene un nombre de zona único globalmente (por ejemplo, contoso.com), a diferencia de la zona privada que debe ser única solo dentro del grupo de recursos?
