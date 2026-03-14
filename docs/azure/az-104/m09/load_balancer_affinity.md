# Load Balancer Affinity (afinidad de sesión)

Es como que en un restaurante con varios camareros siempre te atienda el mismo: todas las peticiones del mismo comensal (misma IP de origen) van al mismo servidor backend. Sin afinidad, cada nueva petición puede ir a un camarero distinto; con afinidad, el mismo cliente mantiene la “mesa” en el mismo backend.

## Definición

La **persistencia de sesión** (session persistence), también llamada **session affinity**, **source IP affinity** o **client IP affinity**, es la opción en la **regla de equilibrio de carga** de Azure Load Balancer que determina si las conexiones del mismo cliente deben ir siempre al mismo backend. Se configura por regla como **Session persistence** y tiene tres modos: None (sin afinidad), Client IP (2-tuple) y Client IP and protocol (3-tuple).

Permite:

- Decidir si el mismo cliente (por IP o por IP + protocolo) va siempre al mismo backend o puede ir a cualquiera
- Soportar aplicaciones con estado en el servidor o sesiones en memoria sin repartir un mismo cliente entre varias VMs
- Resolver escenarios donde un mismo cliente usa TCP y UDP al mismo endpoint y ambos deben ir a la misma VM (ej. RD Gateway, subida de medios)

Para el concepto general de Azure Load Balancer (capa 4, frontend, backend pool, health probe, reglas), ver **Load Balancer**.

## Componentes

**Session persistence (modo en portal)** – Valor por regla de equilibrio de carga: **None**, **Client IP** o **Client IP and protocol**; determina el modo de distribución (hash 5-tuple, 2-tuple o 3-tuple)

**None (hash based, 5-tuple)** – Comportamiento por defecto; hash por IP origen, puerto origen, IP destino, puerto destino, protocolo; el tráfico del mismo cliente puede ir a cualquier backend sano; solo hay “stickiness” dentro de una sesión de transporte (nueva conexión = nuevo puerto origen puede ir a otro backend)

**Client IP (2-tuple)** – Source IP affinity; hash por IP origen e IP destino; las peticiones sucesivas desde la misma IP de origen van al mismo backend

**Client IP and protocol (3-tuple)** – Source IP + protocol; hash por IP origen, IP destino y protocolo (TCP/UDP); mismo cliente IP y mismo protocolo → mismo backend; útil cuando el mismo cliente usa TCP y UDP al mismo endpoint y ambos deben acabar en la misma VM

**loadDistribution (REST API)** – `"Default"` (None), `"SourceIP"` (Client IP), `"SourceIPProtocol"` (Client IP and protocol); no hay downtime al cambiar de modo

## Funcionalidad

1. En cada **regla de equilibrio de carga** del Load Balancer se configura **Session persistence**: None, Client IP o Client IP and protocol
2. Con **None**: cada nueva conexión se asigna según hash 5-tuple; pueden ir a backends distintos
3. Con **Client IP**: todas las conexiones desde la misma IP de origen van al mismo backend (mientras esté sano)
4. Con **Client IP and protocol**: igual pero además se distingue por protocolo; mismo cliente con TCP y UDP puede ir al mismo backend si se desea ese comportamiento
5. Si se añaden o quitan VMs del backend pool, la distribución se recalcula; no se garantiza que conexiones futuras del mismo cliente sigan en el mismo backend

## Casos de Uso

- Aplicaciones con estado en el servidor o sesiones en memoria: usar **Client IP** o **Client IP and protocol** para que el mismo cliente vaya siempre al mismo backend
- Compatibilidad con RD Gateway: **Client IP and protocol** (3-tuple) resuelve incompatibilidades entre Load Balancer y RD Gateway
- Subida de medios con control TCP y datos UDP: canal TCP y sesión UDP del mismo cliente al mismo endpoint deben ir a la misma VM → **Client IP and protocol**

## Errores Comunes

- Confundir **Client IP** con **Client IP and protocol**: el segundo distingue por protocolo (TCP/UDP); si el mismo cliente usa ambos, con 2-tuple pueden ir a backends distintos, con 3-tuple al mismo
- Esperar que la afinidad sobreviva a cambios en el backend pool: al añadir o quitar VMs, la distribución se recalcula y las nuevas conexiones pueden ir a otro backend
- Usar afinidad cuando no hace falta: puede desequilibrar la carga si muchos clientes comparten la misma IP (p. ej. detrás de un proxy)

## Preguntas

1. ¿Session persistence (affinity) en Azure Load Balancer se configura en la regla de equilibrio de carga y puede ser None (5-tuple), Client IP (2-tuple) o Client IP and protocol (3-tuple)?

2. ¿Con Session persistence "Client IP", las peticiones desde la misma IP de origen van al mismo backend; con "None" (default) pueden ir a cualquier backend sano?

3. ¿La diferencia entre Client IP (2-tuple) y Client IP and protocol (3-tuple) es que el segundo además considera el protocolo (TCP/UDP) para asignar al mismo backend?

4. ¿Si se añaden o quitan VMs del backend pool, la distribución se recalcula y no se garantiza que el mismo cliente siga en el mismo backend?

5. ¿Session persistence también se conoce como session affinity, source IP affinity o client IP affinity?

6. ¿Para aplicaciones con estado en el servidor o sesiones en memoria se suele configurar Session persistence Client IP o Client IP and protocol en la regla de equilibrio de carga?
