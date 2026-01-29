# VM Redeploy

## Analogía

VM Redeploy es como cambiar de habitación en el mismo hotel cuando hay mantenimiento en tu piso. Imagina que estás en un hotel enorme y el administrador te dice: "Hay mantenimiento programado en el piso 5, pero puedes moverte al piso 6 que es idéntico". No cambias de hotel, no pierdes tus pertenencias, solo te mueves a otra habitación en el mismo edificio. VM Redeploy funciona igual: cuando Azure tiene mantenimiento programado en el host físico donde está tu VM, puedes usar Redeploy para moverla a otro host físico dentro del mismo centro de datos. Tu VM se reinicia brevemente, pero todos tus datos, configuración y discos se mantienen intactos. Es la forma correcta de evitar el mantenimiento del host sin tener que recrear la VM.

## Definición

VM Redeploy es una operación de Azure que mueve una máquina virtual a otro host físico dentro del mismo centro de datos, reiniciando la VM en el nuevo host sin pérdida de datos.

Permite:

- Mover una VM a otro host físico dentro del mismo centro de datos.
- Evitar mantenimiento programado del host físico original.
- Reiniciar la VM en el nuevo host sin pérdida de datos.
- Mantener todos los discos, configuración y datos intactos.
- Ejecutar la operación sin necesidad de recrear la VM.
- Completar la operación en minutos con downtime mínimo.

## Componentes

**Host Físico** – Servidor físico en el centro de datos de Azure donde se ejecuta la VM.

**Redeploy Operation** – Operación que desasigna la VM del host actual y la asigna a un nuevo host.

**Desasignación** – Proceso que libera la VM del host físico actual.

**Reasignación** – Proceso que asigna la VM a un nuevo host físico disponible.

**Centro de Datos** – Instalación física dentro de una región de Azure donde están los hosts físicos.

**Mantenimiento Programado** – Mantenimiento planificado del host físico que requiere mover VMs.

## Funcionalidad

1. Azure programa mantenimiento en un host físico específico dentro de un centro de datos.
2. Se identifica que una VM está ejecutándose en el host que requiere mantenimiento.
3. Se ejecuta la operación Redeploy desde Azure Portal, PowerShell, CLI o API REST.
4. Azure desasigna la VM del host físico actual, liberando los recursos del host.
5. La VM se reinicia brevemente durante la desasignación.
6. Azure asigna la VM a un nuevo host físico disponible dentro del mismo centro de datos.
7. La VM arranca en el nuevo host con todos los discos, configuración y datos intactos.
8. El mantenimiento se puede realizar en el host original sin afectar la VM.
9. La VM continúa operando normalmente en el nuevo host físico.

## Casos de Uso

- Evitar mantenimiento programado del host físico moviendo la VM a otro host.
- Resolver problemas de conectividad o rendimiento relacionados con el host físico.
- Mover VMs cuando Azure notifica mantenimiento planificado del host.
- Reiniciar VMs en un host diferente sin recrear la infraestructura.
- Evitar downtime prolongado durante mantenimiento de infraestructura física.
- Mover VMs cuando hay problemas de hardware en el host actual.
- Cumplir con requisitos de alta disponibilidad evitando mantenimiento del host.

## Errores Comunes

- Pensar que Redeploy mueve la VM a otra región (solo mueve a otro host en el mismo centro de datos).
- Creer que Redeploy causa pérdida de datos (todos los datos y discos se mantienen intactos).
- Confundir Redeploy con migración a Availability Zone (Redeploy no cambia la zona de disponibilidad).
- Asumir que Redeploy no requiere reinicio (la VM se reinicia brevemente durante la operación).
- Pensar que Redeploy se puede ejecutar en VMs desasignadas (la VM debe estar ejecutándose o desasignada).
- Creer que Redeploy cambia la IP de la VM (la IP se mantiene si la VM no se desasigna completamente).
- Confundir Redeploy con Move (Redeploy es dentro del mismo centro de datos, Move puede cambiar región).
- Asumir que Redeploy resuelve todos los problemas de VM (solo resuelve problemas relacionados con el host físico).

## Preguntas

1. ¿VM Redeploy mueve una VM a otro host físico dentro del mismo centro de datos para evitar mantenimiento programado?.

2. ¿Redeploy reinicia la VM en el nuevo host pero mantiene todos los discos, configuración y datos intactos?.

3. ¿Redeploy es la solución correcta cuando Azure programa mantenimiento en el host físico donde está ejecutándose una VM?.

4. ¿Redeploy no mueve la VM a otra región, solo a otro host físico en el mismo centro de datos?.

5. ¿La operación Redeploy causa un reinicio breve de la VM pero no pérdida de datos?.

6. ¿Redeploy se puede ejecutar desde Azure Portal, PowerShell, CLI o API REST?.

7. ¿Redeploy es útil para resolver problemas de conectividad o rendimiento relacionados con el host físico?.

8. ¿Redeploy mantiene la misma IP de la VM si la VM no se desasigna completamente durante la operación?.
