# Azure Virtual Machines

## Analogía

Azure Virtual Machines es como tener un servidor físico completo en la nube, pero con superpoderes. Imagina que necesitas un servidor para ejecutar tu aplicación. En lugar de comprar hardware físico, instalar el sistema operativo, configurar la red y mantener todo tú mismo, Azure te da una "máquina virtual": un servidor completo que existe solo en software pero funciona exactamente igual que uno físico. Puedes elegir el tamaño (CPU, memoria, almacenamiento), el sistema operativo (Windows, Linux), y Azure se encarga de todo lo demás: la infraestructura física, la red, el almacenamiento. Es como alquilar un servidor completo pero sin las limitaciones físicas: puedes cambiarlo de tamaño, moverlo a otro lugar, hacer copias instantáneas, y todo en minutos.

## Definición

Azure Virtual Machines (VM) es un servicio de infraestructura como servicio (IaaS) que proporciona máquinas virtuales bajo demanda con control completo sobre el sistema operativo y la configuración.

Permite:

- Crear y gestionar máquinas virtuales Windows o Linux con control completo del sistema operativo
- Elegir entre múltiples tamaños de VM optimizados para diferentes cargas de trabajo
- Configurar almacenamiento mediante Managed Disks o Unmanaged Disks
- Conectar VMs a redes virtuales para comunicación con otros recursos
- Escalar verticalmente (cambiar tamaño) o horizontalmente (múltiples instancias)
- Implementar alta disponibilidad mediante Availability Sets o Availability Zones
- Mover VMs entre hosts físicos mediante Redeploy para evitar mantenimiento
- Instalar extensiones de VM para automatización y configuración post-despliegue

## Componentes

**VM Size** – Tamaño de la VM que define CPU, memoria RAM, rendimiento de almacenamiento y red

**Operating System Disk** – Disco que contiene el sistema operativo y se usa para arrancar la VM

**Data Disks** – Discos adicionales conectados a la VM para almacenar datos de aplicaciones

**Network Interface Card (NIC)** – Interfaz de red que conecta la VM a una Virtual Network

**Public IP Address** – Dirección IP pública opcional para acceso desde Internet

**Availability Set** – Agrupación lógica que distribuye VMs en dominios de fallo y actualización

**Availability Zone** – Zona física separada dentro de una región para alta disponibilidad regional

**VM Extensions** – Aplicaciones pequeñas que proporcionan configuración y automatización post-despliegue

**Redeploy** – Operación que mueve una VM a otro host físico dentro del mismo centro de datos

## Funcionalidad

1. Se selecciona una imagen de VM (Windows, Linux o imagen personalizada) desde Azure Marketplace o galería propia
2. Se elige un tamaño de VM según los requisitos de CPU, memoria y rendimiento necesarios
3. Se configura la red conectando la VM a una Virtual Network mediante una Network Interface Card (NIC)
4. Se selecciona el tipo de almacenamiento (Managed Disks recomendado) para el disco del sistema operativo y discos de datos
5. Se configura alta disponibilidad opcional mediante Availability Sets o Availability Zones
6. La VM se crea y se aprovisiona con el sistema operativo seleccionado
7. Se pueden instalar extensiones de VM para automatizar configuración, monitoreo o seguridad
8. Se puede acceder a la VM mediante RDP (Windows) o SSH (Linux) usando credenciales configuradas
9. Se puede mover la VM a otro host físico mediante Redeploy para evitar mantenimiento programado del host

## Casos de Uso

- Migrar aplicaciones desde servidores físicos on-premises a Azure sin cambios en el código
- Ejecutar aplicaciones que requieren control completo del sistema operativo y configuración personalizada
- Hospedar bases de datos, servidores de aplicaciones y servicios que necesitan alta disponibilidad
- Crear entornos de desarrollo y pruebas que se pueden crear y eliminar rápidamente
- Ejecutar cargas de trabajo que requieren rendimiento específico (CPU, memoria, GPU)
- Implementar arquitecturas de alta disponibilidad distribuyendo VMs en Availability Sets o Zones
- Mover VMs entre hosts físicos para evitar mantenimiento programado sin downtime
- Configurar VMs con extensiones para automatizar instalación de software y configuración

## Errores Comunes

- Pensar que las VMs son siempre la mejor opción (PaaS puede ser más adecuado para muchas aplicaciones)
- Confundir Availability Sets con Availability Zones (Sets distribuyen en dominios, Zones en zonas físicas)
- Asumir que Redeploy mueve la VM a otra región (solo mueve a otro host en el mismo centro de datos)
- Creer que se puede cambiar el tamaño de una VM sin reiniciarla (requiere desasignación y reinicio)
- Pensar que Managed Disks y Unmanaged Disks funcionan igual (Managed Disks es más simple y recomendado)
- Confundir escalado vertical (cambiar tamaño) con horizontal (agregar más VMs)
- Asumir que todas las VMs tienen acceso a Internet por defecto (requiere Public IP o NAT Gateway)
- Creer que Redeploy causa pérdida de datos (no causa pérdida, solo reinicia la VM en otro host)

## Preguntas

1. ¿Azure Virtual Machines es un servicio IaaS que proporciona control completo sobre el sistema operativo?

2. ¿Redeploy mueve una VM a otro host físico dentro del mismo centro de datos para evitar mantenimiento programado?

3. ¿Los Availability Sets distribuyen VMs en dominios de fallo y actualización dentro de la misma región?

4. ¿Los Availability Zones son zonas físicas separadas dentro de una región para alta disponibilidad regional?

5. ¿Managed Disks es el tipo de almacenamiento recomendado para VMs en lugar de Unmanaged Disks?

6. ¿Las VM Extensions permiten automatizar configuración y software sin conectarse manualmente a la VM?

7. ¿Se puede cambiar el tamaño de una VM (escalado vertical) pero requiere desasignación y reinicio?

8. ¿Redeploy no causa pérdida de datos y solo reinicia la VM en un host físico diferente?
