# Bicep (Azure)

Bicep es como escribir los mismos planos de infraestructura que las plantillas ARM (JSON), pero en un idioma más corto y legible. En lugar de escribir mucho JSON con llaves y comas, defines recursos, parámetros y módulos con una sintaxis más clara; el compilador de Bicep traduce tu archivo a una plantilla ARM en JSON que Azure despliega igual que siempre. No es un motor distinto: es la misma implementación que las plantillas ARM, solo que con otra sintaxis. Lo que defines (VMs, redes, almacenamiento) y el resultado del despliegue son los mismos; cambia la forma de escribirlo.

## Definición

Bicep es un lenguaje de dominio (DSL) de Microsoft para definir infraestructura de Azure de forma declarativa; compila a plantillas ARM (JSON) y se despliega mediante el mismo motor que las plantillas ARM; ofrece sintaxis más concisa y legible que el JSON de ARM sin perder capacidades.

Permite:

- Definir recursos de Azure (VMs, redes, almacenamiento, etc.) en archivos .bicep con sintaxis declarativa más corta que el JSON de ARM
- Usar parámetros, variables y outputs igual que en plantillas ARM (mismo modelo de despliegue)
- Organizar y reutilizar código mediante módulos (archivos .bicep que se invocan desde otros)
- Compilar a JSON (bicep build) para revisar o desplegar la plantilla ARM generada, o desplegar directamente el .bicep (Azure compila en el servicio)
- Decompilar una plantilla ARM (JSON) a Bicep (bicep decompile) para migrar plantillas existentes a sintaxis Bicep o como punto de partida para edición
- Integrarse con pipelines CI/CD y con las mismas herramientas de despliegue que las plantillas ARM (CLI, PowerShell, Portal)

## Componentes

**Archivo .bicep** – Archivo de texto con sintaxis Bicep que define recursos, parámetros, variables, outputs y opcionalmente módulos; se compila a una plantilla ARM (JSON) o se despliega directamente

**Resource (recurso)** – Declaración de un recurso de Azure en Bicep (tipo, nombre, propiedades); equivale a un recurso en la sección resources de una plantilla ARM

**Parameters (parámetros)** – Valores configurables que se pasan al desplegar (nombres, tamaños, entornos); soportan tipos (string, int, bool, object, array) y decoradores para validación o valores seguros

**Variables** – Valores calculados o reutilizables dentro del archivo Bicep para simplificar expresiones

**Outputs** – Valores que se devuelven después del despliegue (IPs, nombres, endpoints); equivalentes a la sección outputs de una plantilla ARM

**Module (módulo)** – Invocación de otro archivo .bicep desde el archivo actual; permite reutilizar y componer plantillas (p. ej. un módulo para la red, otro para las VMs); los módulos se compilan como plantillas anidadas en ARM

**Compilación (bicep build)** – Proceso que traduce el archivo .bicep a una plantilla ARM en JSON; se puede ejecutar localmente con Bicep CLI o en el servicio al desplegar directamente el .bicep

**Decompilación (bicep decompile)** – Proceso inverso a la compilación: toma una plantilla ARM (JSON) y genera un archivo .bicep equivalente; útil para migrar plantillas existentes a Bicep o para obtener sintaxis Bicep como punto de partida; el resultado puede requerir ajustes manuales según la complejidad del JSON

**ARM template (salida)** – La plantilla JSON generada por la compilación de Bicep; es una plantilla ARM estándar que se puede desplegar con las mismas herramientas que cualquier plantilla ARM

## Funcionalidad

1. Se escribe un archivo .bicep con la definición de recursos, parámetros, variables y outputs (y opcionalmente módulos que referencian otros .bicep)
2. Opcionalmente se compila localmente con `bicep build` para obtener el JSON equivalente y validar la sintaxis; o bien se decompila una plantilla ARM existente con `bicep decompile <archivo.json>` para obtener un .bicep a partir del JSON
3. Se despliega el archivo .bicep mediante Azure CLI (`az deployment group create --template-file main.bicep`), PowerShell o el Portal; si se pasa un .bicep, Azure compila en el servicio y despliega la plantilla ARM resultante
4. Los parámetros se pasan en la línea de comandos, en un archivo de parámetros (.bicepparam o JSON) o con valores por defecto definidos en el archivo
5. El motor de despliegue de ARM procesa la plantilla (ya sea el JSON generado por Bicep o el JSON de una plantilla ARM clásica) y crea o actualiza los recursos de forma idempotente
6. Los módulos permiten dividir la infraestructura en archivos reutilizables (p. ej. módulo de red, módulo de almacenamiento) y componerlos en un archivo principal
7. Bicep y las plantillas ARM comparten el mismo modelo de recursos y el mismo motor de despliegue; no hay diferencias de comportamiento en el despliegue, solo en la sintaxis de autoría

## Casos de Uso

- Escribir infraestructura como código con sintaxis más legible que el JSON de ARM
- Reutilizar lógica mediante módulos (red, almacenamiento, VMs) en varios despliegues
- Parametrizar nombres, tamaños y entornos para los mismos conceptos que en plantillas ARM
- Integrar con pipelines CI/CD desplegando archivos .bicep o el JSON compilado
- Compilar a JSON para revisar la plantilla ARM generada o para despliegues que exigen un archivo JSON
- Decompilar plantillas ARM (JSON) existentes a Bicep con `bicep decompile` para migrar a Bicep o como punto de partida sin reescribir todo el JSON
- Mantener un solo lenguaje (Bicep) para autoría y dejar que el servicio o la CLI compilen a ARM en el despliegue

## Errores Comunes

- Confundir Bicep con un motor de despliegue distinto (Bicep compila a ARM; el despliegue lo hace el mismo motor que las plantillas ARM)
- Pensar que Bicep puede definir recursos que ARM no soporta (Bicep y ARM tienen el mismo conjunto de tipos de recursos y propiedades)
- Creer que hace falta compilar siempre a JSON antes de desplegar (Azure CLI y PowerShell pueden desplegar un .bicep directamente; el servicio compila)
- Usar sintaxis JSON de ARM dentro de un archivo .bicep (Bicep tiene su propia sintaxis; no se mezcla JSON de plantilla ARM en un .bicep)
- Olvidar que los módulos Bicep se traducen a implementaciones anidadas de plantillas ARM (límites de anidación y tamaño de ARM siguen aplicando)
- Esperar que `bicep decompile` produzca siempre un Bicep idéntico en comportamiento sin revisar (el resultado puede requerir ajustes según la complejidad del JSON)

## Preguntas

1. ¿Bicep es un lenguaje de dominio (DSL) que compila a plantillas ARM (JSON) y se despliega con el mismo motor que las plantillas ARM?

2. ¿Bicep permite definir recursos, parámetros, variables y outputs con sintaxis más concisa que el JSON de ARM?

3. ¿Los módulos en Bicep permiten invocar otros archivos .bicep para reutilizar y componer plantillas?

4. ¿Se puede desplegar un archivo .bicep directamente con Azure CLI o PowerShell sin compilar antes a JSON (el servicio compila)?

5. ¿Bicep y las plantillas ARM comparten el mismo modelo de recursos y el mismo motor de despliegue?

6. ¿La compilación de Bicep (bicep build) genera una plantilla ARM en JSON estándar que se puede desplegar con las mismas herramientas que cualquier plantilla ARM?

7. ¿La decompilación (bicep decompile) toma una plantilla ARM en JSON y genera un archivo .bicep equivalente para migrar o como punto de partida?
