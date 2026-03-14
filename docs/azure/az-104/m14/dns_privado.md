# DNS privado (Azure DNS Private Zones)

## Analogía

DNS privado en Azure es como una guía telefónica interna de tu empresa: solo quien está dentro de la red (las VNets que tú enlazas) puede consultarla. Los nombres que defines (por ejemplo, mi-servidor.contoso.local) resuelven a IPs privadas y no se publican en Internet. Puedes enlazar varias redes virtuales a la misma zona privada para que todas resuelvan los mismos nombres. Opcionalmente, cuando creas una VM en una VNet enlazada, Azure puede registrar automáticamente su nombre e IP en la zona, para no tener que crear registros a mano.

## Definición

Azure DNS Private Zones (zonas DNS privadas) es el servicio de Azure que permite hospedar zonas DNS que solo se resuelven dentro de las redes virtuales que enlazas a la zona; los registros no son visibles en Internet y los nombres resuelven a IPs privadas; opcionalmente se puede habilitar el registro automático de VMs en la zona.

Permite:

- Crear zonas DNS privadas (por ejemplo, contoso.local, internal.empresa.com) cuyos registros solo se resuelven desde las VNets enlazadas
- Enlazar una o más redes virtuales a la zona mediante "virtual network links"; solo las VMs y recursos de esas VNets pueden resolver los nombres de la zona
- Resolver nombres a IPs privadas sin exponer información DNS a Internet
- Habilitar registro automático (autoregistration) en el enlace: cuando se crea, modifica o elimina una VM en la VNet enlazada, Azure crea, actualiza o elimina el registro A correspondiente en la zona
- Usar los mismos tipos de registros que en DNS público (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT) dentro de la zona privada
- Compartir la misma zona privada entre varias VNets (por ejemplo, hub y spokes) para resolución de nombres común

## Componentes

**Zona DNS privada (Private DNS zone)** – Recurso de Azure que representa una zona DNS privada; contiene registros (A, AAAA, CNAME, etc.) que solo se resuelven desde las VNets enlazadas; el nombre de la zona debe ser único dentro del grupo de recursos (no tiene que ser único globalmente como en DNS público)

**Virtual network link (enlace de red virtual)** – Asociación entre la zona privada y una VNet; las consultas DNS desde esa VNet pueden resolver los registros de la zona; cada enlace puede habilitar o no el registro automático

**Registro automático (autoregistration)** – Opción del enlace que hace que Azure cree, actualice o elimine registros A (y PTR opcional) en la zona cuando se crean, modifican o eliminan VMs en la VNet enlazada; la VM se registra con su nombre de host y su IP privada

**Resolución privada** – Las consultas DNS desde las VNets enlazadas resuelven los nombres de la zona a las IPs definidas en los registros; las consultas desde fuera de las VNets enlazadas no obtienen respuesta de esta zona

**No visible en Internet** – Los registros de la zona privada no se publican en los servidores DNS públicos; solo son accesibles desde las VNets enlazadas

**Registros** – Entradas en la zona (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT) que definen la resolución de nombres; se crean manualmente o por registro automático (solo A/PTR para VMs)

## Funcionalidad

1. Se crea una zona DNS privada en un grupo de recursos (nombre de zona, por ejemplo contoso.local)
2. Se crea un virtual network link entre la zona privada y una o más VNets; opcionalmente se habilita registro automático en cada enlace
3. Se añaden registros a la zona manualmente (A, AAAA, CNAME, MX, etc.) o se deja que el registro automático cree registros A (y PTR) cuando se crean VMs en las VNets enlazadas
4. Las VMs y recursos de las VNets enlazadas configuran su DNS para usar el DNS de Azure (o el resolver que apunte a la zona); las consultas a nombres de la zona resuelven a las IPs definidas en los registros
5. Las consultas desde VNets no enlazadas o desde Internet no resuelven los nombres de la zona privada
6. La zona privada puede estar enlazada a VNets de la misma suscripción o de otras suscripciones (según permisos)
7. Si se usa registro automático, al eliminar una VM se elimina su registro A (y PTR si aplica) de la zona

## Casos de Uso

- Resolver nombres de recursos internos (VMs, Private Endpoints) por nombre en lugar de por IP dentro de la VNet
- Compartir una misma zona privada entre varias VNets (hub-and-spoke) para que todas resuelvan los mismos nombres internos
- Usar registro automático para que las VMs aparezcan en DNS sin crear registros manualmente
- Evitar que la resolución de nombres internos sea visible o accesible desde Internet
- Resolver nombres de servicios PaaS con Private Endpoint (por ejemplo, cuenta de almacenamiento) en una zona privada vinculada a la VNet

## Errores Comunes

- Confundir zona DNS privada con zona DNS pública (la privada solo se resuelve desde las VNets enlazadas; la pública es autoritativa en Internet)
- Creer que la zona privada es visible en Internet (no lo es; solo las VNets enlazadas pueden resolverla)
- Olvidar crear el virtual network link (sin enlace, ninguna VNet puede resolver la zona)
- Pensar que el registro automático crea cualquier tipo de registro (solo crea A y opcionalmente PTR para VMs; el resto hay que crearlo manualmente)
- Enlazar una VNet que ya usa otro DNS para el mismo nombre de zona y esperar que la zona privada tenga prioridad (depende de la configuración DNS de la VNet; la VNet debe usar el resolver que consulta la zona privada)

## Preguntas

1. ¿Una zona DNS privada de Azure solo se resuelve desde las redes virtuales enlazadas a la zona (virtual network links)?

2. ¿Los registros de una zona DNS privada no son visibles en Internet y resuelven a IPs privadas?

3. ¿El registro automático (autoregistration) en el enlace crea o actualiza registros A (y PTR) en la zona cuando se crean, modifican o eliminan VMs en la VNet enlazada?

4. ¿Se puede enlazar la misma zona privada a varias VNets para que todas resuelvan los mismos nombres?

5. ¿La zona DNS privada puede contener los mismos tipos de registros que una zona pública (A, AAAA, CNAME, MX, PTR, SOA, SRV, TXT)?

6. ¿Sin virtual network link ninguna VNet puede resolver los nombres de la zona privada?
