# Network Security Group (NSG)

## Analogía

Un Network Security Group es como un guardia de seguridad en la entrada de un edificio que revisa a cada persona antes de dejarla entrar o salir. Imagina que tienes un edificio con múltiples puertas y cada una tiene un guardia con una lista de reglas. El guardia verifica: ¿de dónde vienes? (dirección IP), ¿a qué puerta quieres ir? (puerto), ¿qué tipo de comunicación es? (protocolo). Si cumples con las reglas permitidas, pasas. Si no, te bloquea. Este guardia puede estar en la entrada principal del edificio (subred) o en la puerta de tu oficina específica (NIC). Siempre está vigilando y aplicando las mismas reglas sin excepción.

## Definición

Un Network Security Group (NSG) es un recurso de Azure que actúa similar un firewall de red que contiene reglas que permiten o deniegan el tráfico de red entrante y saliente.

Permite:

- Controlar el tráfico basado en dirección IP de origen y destino
- Filtrar por puertos y protocolos específicos
- Aplicar reglas de seguridad a nivel de subred o interfaz de red (NIC)
- Permitir o denegar tráfico según reglas configuradas
- Proteger recursos de red contra acceso no autorizado

## Componentes

**Reglas de Entrada (Inbound)** – Reglas que controlan el tráfico que llega al recurso

**Reglas de Salida (Outbound)** – Reglas que controlan el tráfico que sale del recurso

**Dirección IP de Origen/Destino** – Dirección IP o rango de IPs que se evalúa en la regla

**Puerto** – Puerto o rango de puertos que se evalúa en la regla

**Protocolo** – Protocolo de red (TCP, UDP, ICMP, etc.) que se evalúa en la regla

**Prioridad** – Número que determina el orden de evaluación de las reglas (menor número = mayor prioridad)

**Acción** – Permite o deniega el tráfico que coincide con la regla

## Funcionalidad

1. Se crea un NSG con reglas de entrada y salida definidas
2. El NSG se asocia a una subred o a una interfaz de red (NIC) de una VM
3. Cuando llega tráfico, el NSG evalúa las reglas en orden de prioridad
4. Se evalúa primero la dirección IP de origen o destino
5. Luego se evalúa el puerto y el protocolo
6. Si el tráfico coincide con una regla, se aplica la acción (permitir o denegar)
7. Si no coincide con ninguna regla, se aplica la regla por defecto (denegar todo)

## Casos de Uso

- Restringir acceso SSH/RDP solo desde direcciones IP específicas
- Permitir tráfico web (puerto 80/443) solo desde Internet
- Bloquear tráfico entre subredes internas para segmentación de red
- Permitir comunicación entre VMs en la misma subred
- Proteger bases de datos permitiendo acceso solo desde subredes de aplicación
- Implementar modelo de seguridad de red de confianza cero

## Preguntas

1. ¿Un NSG puede aplicarse tanto a una subred como a una interfaz de red (NIC) de una VM?

2. ¿Las reglas de un NSG evalúan el tráfico basándose en dirección IP, puerto y protocolo?

3. ¿Qué ocurre con el tráfico que no coincide con ninguna regla configurada en un NSG?

4. ¿Un NSG puede tener reglas que permitan y reglas que denieguen tráfico simultáneamente?

5. ¿La prioridad de las reglas en un NSG determina el orden en que se evalúan?
