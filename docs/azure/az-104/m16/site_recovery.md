# Azure Site Recovery

## Analogía

Azure Site Recovery es como tener una copia de seguridad completa de tu oficina en otra ciudad, pero mucho más inteligente. Imagina que tu oficina principal tiene un desastre: un incendio, un terremoto o cualquier catástrofe. En lugar de perder todo y empezar de cero, tienes una oficina gemela en otra ciudad con todos tus documentos, computadoras y sistemas ya preparados. Esta oficina secundaria está apagada para ahorrar costos, pero tiene todo listo. Cuando ocurre el desastre, solo necesitas "encender" la oficina secundaria y en minutos estás operando de nuevo, casi sin perder información.

## Definición

Azure Site Recovery es un servicio de recuperación ante desastres que replica máquinas virtuales y aplicaciones a una región secundaria para garantizar la continuidad del negocio.

Permite:

- Replicación continua de VMs a otra región de Azure
- Tiempo de recuperación (RTO) de minutos
- Objetivos de punto de recuperación (RPO) de segundos a minutos
- VMs secundarias apagadas hasta que se necesiten
- Activación automática o manual mediante planes de recuperación

## Componentes

**Replicación Continua** – Proceso que copia constantemente los cambios de las VMs primarias a la región secundaria

**Plan de Recuperación** – Documento digital, script o flujo que define cómo activar las VMs secundarias durante un failover

**RPO (Recovery Point Objective)** – Cantidad máxima de datos que se está dispuesto a perder (segundos o minutos)

**RTO (Recovery Time Objective)** – Tiempo máximo que se puede estar fuera de servicio antes de recuperar operaciones

**Failover** – Proceso de conmutación por error que transfiere el control a la región secundaria cuando la primaria falla

**Failback** – Proceso de regresar las operaciones a las VMs principales cuando el problema se resuelve

**VMs Secundarias** – Máquinas virtuales en la región secundaria que permanecen apagadas hasta el failover

## Funcionalidad

1. Se configura Azure Site Recovery para replicar VMs de una región primaria a una secundaria
2. El servicio replica continuamente los cambios de las VMs primarias a la región secundaria
3. Las VMs secundarias se crean pero permanecen apagadas para reducir costos
4. Se define un plan de recuperación que especifica el orden y configuración de activación
5. En caso de desastre, se ejecuta el failover activando las VMs secundarias
6. El tiempo de recuperación es de minutos, con pérdida mínima de datos según el RPO configurado
7. Una vez resuelto el problema, se ejecuta failback para regresar a las VMs primarias

## Casos de Uso

- Proteger aplicaciones críticas de negocio con replicación entre regiones
- Cumplir requisitos de continuidad del negocio y recuperación ante desastres
- Reducir tiempo de inactividad en caso de fallos de infraestructura
- Realizar pruebas de recuperación sin interrumpir operaciones
- Migrar VMs entre regiones de Azure de forma controlada
- Proteger cargas de trabajo híbridas replicando desde on-premises a Azure

## Preguntas

1. ¿Azure Site Recovery mantiene las VMs secundarias encendidas constantemente o solo las activa durante un failover?

2. ¿Qué es el RPO y qué valores ofrece Azure Site Recovery para este objetivo?

3. ¿Un plan de recuperación define cómo se activan las VMs secundarias durante un failover?

4. ¿Cuál es la diferencia entre failover y failback en Azure Site Recovery?

5. ¿Azure Site Recovery puede lograr un tiempo de recuperación (RTO) de minutos para restaurar operaciones?
