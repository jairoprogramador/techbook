# Azure CLI

## Analogía

Azure CLI es como la consola de comandos con la que le hablas a Azure desde tu máquina: en lugar de hacer clic en el portal, escribes órdenes en la terminal y Azure ejecuta las acciones. Sirve para automatizar tareas, desplegar recursos y aplicar configuraciones desde scripts, y funciona igual en Linux, Windows y macOS. No es el portal ni PowerShell: es otra herramienta oficial de Microsoft para gestionar Azure desde línea de comandos.

## Definición

Azure CLI es la interfaz de línea de comandos multiplataforma de Microsoft para gestionar recursos de Azure; invoca las APIs REST de Azure y permite automatización, scripting y configuraciones avanzadas que a veces no están disponibles en el portal o en cmdlets básicos de PowerShell.

Permite:

- Ejecutar comandos `az` desde Linux, Windows y macOS para crear, modificar y eliminar recursos de Azure
- Automatizar despliegues y operaciones mediante scripts (bash, PowerShell, etc.)
- Aplicar configuración personalizada durante el despliegue: datos personalizados (custom data), cloud-init para VMs Linux (p. ej. Ubuntu), inyección de certificados CA o secretos en el aprovisionamiento
- Acceder a parámetros y opciones avanzadas que no siempre están expuestos en el portal o en cmdlets de PowerShell de alto nivel
- Integrar con pipelines CI/CD y entornos donde la interfaz es solo terminal (servidores, contenedores, WSL)

## Componentes

**Comando `az`** – Ejecutable principal de Azure CLI; todos los comandos comienzan por `az` seguido del grupo de recursos y la operación (p. ej. `az vm create`, `az group list`)

**Login y contexto** – `az login` para autenticarse; `az account set` para elegir suscripción; el contexto (tenant, suscripción) se mantiene en la sesión

**Extensiones** – Módulos opcionales que añaden comandos (p. ej. `az extension add --name <nombre>`); algunas funcionalidades nuevas aparecen primero como extensión

**Custom data (--custom-data)** – Parámetro en comandos como `az vm create` que permite pasar datos al aprovisionamiento (script cloud-init en base64 para Linux, o script para Windows); la VM los ejecuta en el primer arranque

**Cloud-init** – Estándar de configuración inicial en VMs Linux (Ubuntu, etc.); se suele inyectar vía `--custom-data` con el contenido del script cloud-init en base64; permite instalar paquetes, añadir usuarios, montar discos, agregar certificados CA, etc.

**Certificados CA y secretos** – Se pueden inyectar durante el despliegue mediante custom data (cloud-init), Key Vault references en plantillas ARM/Bicep, o parámetros específicos del CLI según el recurso

**Compatibilidad multiplataforma** – Azure CLI funciona en Linux, Windows y macOS; misma sintaxis y mismos comandos; útil para equipos heterogéneos o servidores sin interfaz gráfica

**Parámetros avanzados** – Muchos comandos exponen opciones (flags) que en el portal equivalen a configuraciones avanzadas o que no tienen equivalente directo en cmdlets de PowerShell básicos; permite control fino desde scripts

## Funcionalidad

1. Se instala Azure CLI en el sistema (Linux, Windows o macOS) según el método oficial (apt, yum, MSI, Homebrew, etc.)
2. Se ejecuta `az login` para autenticarse con Azure (navegador o dispositivo); opcionalmente `az account set --subscription <id>` para elegir suscripción
3. Se ejecutan comandos `az <recurso> <operación>` para crear o gestionar recursos (grupos de recursos, VMs, redes, almacenamiento, etc.)
4. Para configuración personalizada durante el despliegue de una VM Linux (p. ej. Ubuntu): se prepara un script cloud-init (YAML o script) y se codifica en base64; se pasa con `az vm create ... --custom-data <archivo_base64>`
5. Cloud-init se ejecuta en el primer arranque de la VM: instala paquetes, crea usuarios, añade certificados CA, ejecuta scripts; todo definido en el mismo custom data
6. Para certificados CA u otros secretos se puede: incluirlos en el script cloud-init (inline o descargándolos desde una URL segura), o usar referencias a Key Vault en plantillas ARM/Bicep desplegadas con CLI
7. Los parámetros avanzados del CLI (p. ej. opciones de red, almacenamiento, extensiones) permiten configuraciones que a veces no están en el portal o requieren varios pasos en PowerShell
8. Los scripts que usan `az` son reutilizables y pueden ejecutarse en cualquier sistema con Azure CLI instalado (Linux, Windows, macOS)

## Casos de Uso

- Automatizar la creación de recursos (grupos de recursos, VMs, redes) desde scripts en bash o PowerShell
- Desplegar VMs Linux (Ubuntu, etc.) con cloud-init vía `--custom-data` para instalar software, usuarios, certificados CA o configuraciones en el primer arranque
- Añadir certificados CA o secretos durante el aprovisionamiento usando custom data (cloud-init) o integración con Key Vault
- Usar opciones avanzadas del CLI que no están en el portal o en cmdlets de PowerShell básicos
- Ejecutar la misma secuencia de comandos en Linux, Windows y macOS (equipos multiplataforma, CI/CD, WSL)
- Integrar Azure CLI en pipelines de CI/CD o en contenedores para desplegar o configurar recursos sin interfaz gráfica

## Errores Comunes

- Confundir Azure CLI con Azure PowerShell (CLI usa comandos `az` y sintaxis distinta; PowerShell usa cmdlets como `New-AzVm`; ambos gestionan Azure pero son herramientas diferentes)
- Pasar custom data en texto plano sin codificar en base64 cuando el servicio lo requiere (para `--custom-data` en VMs Linux con cloud-init, normalmente se espera base64)
- Creer que cloud-init funciona en cualquier distro (cloud-init es estándar en muchas distros Linux como Ubuntu; en Windows no se usa cloud-init, sino otras mecanismos como custom script extension)
- Asumir que todos los parámetros del portal están en el CLI (en general el CLI tiene igual o más opciones; algunos flujos del portal pueden agrupar varias operaciones)
- Usar Azure CLI sin haber hecho `az login` o sin haber seleccionado la suscripción correcta (`az account show` para comprobar)

## Preguntas

1. ¿Azure CLI es la interfaz de línea de comandos multiplataforma de Microsoft para gestionar recursos de Azure?

2. ¿Azure CLI funciona en Linux, Windows y macOS con la misma sintaxis de comandos `az`?

3. ¿El parámetro `--custom-data` en comandos como `az vm create` permite pasar datos al aprovisionamiento (p. ej. script cloud-init en base64 para VMs Linux)?

4. ¿Cloud-init es un estándar de configuración inicial en VMs Linux (como Ubuntu) que se puede inyectar vía custom data para instalar paquetes, usuarios o certificados CA en el primer arranque?

5. ¿Azure CLI puede exponer parámetros y opciones avanzadas que no siempre están en el portal o en cmdlets básicos de PowerShell?

6. ¿Para automatizar despliegues con configuración personalizada (certificados CA, cloud-init) se suele usar custom data junto con Azure CLI o plantillas ARM/Bicep?
