Su empresa tiene una aplicación web implementada en Azure. Esta aplicación web se distribuye en tres capas diferentes, con tres máquinas virtuales (VM) en cada capa. Además, la aplicación web tiene una dirección IP pública que permite a los clientes acceder a ella.

Está implementando un plan de continuidad empresarial y recuperación ante desastres (BCDR) para esta aplicación web mediante Azure Site Recovery. Ha configurado la replicación de las VM en la región de Azure que hospeda su aplicación web.

Necesita minimizar el objetivo de tiempo de recuperación (RTO).
¿Cuáles cuatro acciones debería realizar en secuencia?

##Solución
1. Crear un plan de recuperación.
2. Personaliza el plan y agrega un paso para adjuntar la dirección IP pública
3. Configurar grupos de seguridad de red (NSG) en la region de destino.
4. Crear un perfil de Traffico Manager

