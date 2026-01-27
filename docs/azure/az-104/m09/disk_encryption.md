# Azure Disk Encryption

## Analogía

Azure Disk Encryption es como tener una caja fuerte para cada disco de tu computadora. Imagina que tienes varios discos duros con información importante. En lugar de dejarlos abiertos donde cualquiera puede leerlos, cada disco tiene su propia cerradura especial. Solo quien tenga la llave correcta puede acceder a los datos. Si alguien roba el disco físico, no podrá leer nada porque está completamente cifrado. La llave se guarda en un lugar muy seguro separado del disco.

## Definición

Azure Disk Encryption es un servicio que cifra los discos de las máquinas virtuales usando tecnologías de cifrado del sistema operativo.

Permite:

- Cifrado del disco del sistema operativo y discos de datos
- Uso de BitLocker para Windows y DM-Crypt para Linux
- Almacenamiento seguro de claves en Azure Key Vault
- Protección de datos en reposo contra acceso no autorizado

## Componentes

**BitLocker (Windows)** – Tecnología de cifrado de Microsoft para discos de Windows

**DM-Crypt (Linux)** – Sistema de cifrado para discos de Linux

**Azure Key Vault** – Servicio que almacena y gestiona las claves de cifrado

**Extensiones de VM** – Extensiones que se instalan en la VM para habilitar el cifrado

**Claves de Cifrado (KEK)** – Claves maestras que protegen las claves de cifrado de disco

## Funcionalidad

1. Se crea o configura un Azure Key Vault para almacenar las claves de cifrado
2. Se habilita Azure Disk Encryption en la máquina virtual
3. Se instala la extensión de cifrado en la VM (BitLocker o DM-Crypt)
4. El servicio genera claves de cifrado y las almacena en Key Vault
5. Los discos se cifran usando las claves almacenadas en Key Vault
6. La VM requiere autenticación con Key Vault para arrancar y descifrar los discos

## Casos de Uso

- Cumplir requisitos de cumplimiento que exigen cifrado de discos
- Proteger datos sensibles en VMs de producción
- Cumplir con estándares de seguridad como HIPAA o PCI-DSS
- Proteger contra acceso físico no autorizado a discos
- Cifrar discos de VMs que almacenan información confidencial

## Preguntas

1. ¿Azure Disk Encryption cifra tanto el disco del sistema operativo como los discos de datos de una VM?

2. ¿Azure Disk Encryption usa BitLocker para cifrar discos de máquinas virtuales Windows?

3. ¿Dónde se almacenan las claves de cifrado utilizadas por Azure Disk Encryption?

4. ¿Es necesario tener un Azure Key Vault configurado antes de habilitar Azure Disk Encryption en una VM?

5. ¿Los discos cifrados con Azure Disk Encryption requieren autenticación con Key Vault para que la VM pueda arrancar?
