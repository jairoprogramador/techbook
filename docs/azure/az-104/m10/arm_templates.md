# Plantillas ARM

## Analogía

Las plantillas ARM son como planos arquitectónicos detallados que le dices a Azure exactamente qué construir y cómo. Imagina que quieres construir una casa completa: en lugar de ir comprando materiales y construyendo habitación por habitación manualmente, tienes un plano que especifica cada detalle: cuántas habitaciones, dónde van las ventanas, qué tipo de cableado, qué instalaciones. Las plantillas ARM funcionan igual: defines en código JSON qué recursos necesitas (VMs, redes, almacenamiento) y Azure los construye todos de una vez. Pero hay algo más inteligente: puedes incluir "instrucciones de configuración" dentro de esos planos. Por ejemplo, si defines una VM con Windows Server, el sistema operativo es como el cuerpo de la casa, pero las Extensiones de VM son como las instrucciones que le dices al constructor: "cuando termines de construir la casa, instala automáticamente el servidor web IIS ejecutando este script de PowerShell". Así, cuando Azure crea la VM, automáticamente ejecuta esas instrucciones sin que tengas que conectarte manualmente.

## Definición

Las plantillas ARM son archivos JSON declarativos que definen la infraestructura y configuración de recursos de Azure que se implementarán de forma idempotente y reproducible.

Permite:

- Definir infraestructura completa (VMs, redes, almacenamiento) en código JSON declarativo
- Implementar recursos de forma idempotente (mismo resultado cada vez que se ejecuta)
- Automatizar configuración post-despliegue mediante extensiones de VM
- Reutilizar plantillas para replicar entornos (dev, staging, prod)
- Integrar con pipelines CI/CD para despliegues automatizados
- Parametrizar valores para flexibilidad en diferentes entornos
- Ejecutar scripts personalizados durante el aprovisionamiento mediante Custom Script Extension

## Componentes

**Estructura JSON** – Archivo JSON con secciones: $schema, contentVersion, parameters, variables, resources y outputs

**Parameters** – Valores configurables que se pasan al desplegar la plantilla (nombres, tamaños, configuraciones)

**Variables** – Valores calculados o reutilizables dentro de la plantilla para simplificar expresiones complejas

**Resources** – Definiciones de recursos de Azure que se crearán (VMs, redes, almacenamiento, etc.)

**Outputs** – Valores que se devuelven después del despliegue (IPs, nombres, endpoints)

**ExtensionProfile** – Sección dentro de recursos de VM o VM Scale Sets que define extensiones de VM a instalar automáticamente

**Custom Script Extension** – Extensión que ejecuta scripts personalizados (PowerShell en Windows, Bash en Linux) durante o después del aprovisionamiento

**VM Extensions** – Aplicaciones pequeñas que proporcionan configuración post-despliegue y automatización en VMs

**Protected Settings** – Sección segura en extensiones para pasar secretos y valores sensibles sin exponerlos en texto plano

## Funcionalidad

1. Se escribe una plantilla ARM en JSON declarativo definiendo los recursos deseados y su configuración
2. Se definen parámetros para valores que pueden variar entre despliegues (nombres, tamaños, entornos)
3. En recursos de VM o VM Scale Sets, se configura extensionProfile dentro de la definición del recurso
4. Dentro de extensionProfile, se especifican extensiones como Custom Script Extension con su configuración
5. Custom Script Extension se configura con la ubicación del script (URL de Azure Storage, GitHub, etc.) y comandos a ejecutar
6. Cuando Azure crea la VM o instancia del VM Scale Set, automáticamente instala y ejecuta las extensiones configuradas
7. Custom Script Extension descarga el script desde la ubicación especificada y lo ejecuta en la VM
8. Los valores sensibles se pasan mediante protectedSettings que se cifran y no se exponen en texto plano
9. La plantilla se despliega mediante Azure Portal, PowerShell, CLI o APIs REST, creando todos los recursos definidos

## Casos de Uso

- Automatizar instalación de roles de servidor (IIS, SQL Server) durante el aprovisionamiento de VMs Windows Server
- Configurar aplicaciones y servicios en VMs Linux mediante scripts Bash ejecutados automáticamente
- Instalar software y dependencias en instancias de VM Scale Sets cuando se escalan automáticamente
- Configurar VMs con extensiones de monitoreo, seguridad o backup automáticamente durante el despliegue
- Replicar entornos completos (dev, staging, prod) usando la misma plantilla con diferentes parámetros
- Integrar despliegues de infraestructura en pipelines CI/CD para automatización completa
- Desplegar infraestructura como código desde repositorios Git con control de versiones
- Configurar VMs con scripts personalizados sin necesidad de conectarse manualmente después del despliegue

## Errores Comunes

- Pensar que las plantillas ARM requieren programación (usan sintaxis declarativa JSON, no scripts imperativos)
- Configurar extensiones fuera de extensionProfile (deben estar dentro de extensionProfile en VM o VM Scale Sets)
- Pasar secretos en la sección settings en lugar de protectedSettings (settings se expone en texto plano)
- Asumir que las extensiones se ejecutan antes de que la VM esté completamente aprovisionada (se ejecutan después del arranque)
- Creer que Custom Script Extension solo funciona con scripts locales (puede descargar desde URLs, Azure Storage, GitHub)
- Confundir extensionProfile con otras secciones de la plantilla (extensionProfile es específica para extensiones de VM)
- Pensar que las extensiones solo funcionan en VMs individuales (también funcionan en VM Scale Sets mediante extensionProfile)
- Asumir que las extensiones se ejecutan solo una vez (se pueden configurar para ejecutarse en cada instancia nueva de un VM Scale Set)

## Preguntas

1. ¿Las plantillas ARM usan sintaxis declarativa JSON para definir infraestructura sin escribir scripts de programación?

2. ¿extensionProfile es la sección dentro de recursos de VM o VM Scale Sets donde se configuran extensiones de VM?

3. ¿Custom Script Extension ejecuta scripts personalizados (PowerShell o Bash) automáticamente durante el aprovisionamiento de VMs?

4. ¿Para instalar roles de servidor web (IIS) en Windows Server durante el aprovisionamiento, se debe configurar Custom Script Extension dentro de extensionProfile?

5. ¿Los valores sensibles como contraseñas deben pasarse mediante protectedSettings en lugar de settings para evitar exposición en texto plano?

6. ¿Cuando Azure crea una nueva instancia en un VM Scale Set, automáticamente ejecuta las extensiones configuradas en extensionProfile?

7. ¿Custom Script Extension puede descargar scripts desde URLs, Azure Storage o repositorios Git para ejecutarlos en la VM?

8. ¿Las extensiones de VM se ejecutan después de que la VM arranca, no durante la creación del disco del sistema operativo?
