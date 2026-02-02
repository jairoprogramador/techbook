# Presupuestos (Azure Cost Management)

## Analogía

Un presupuesto en Azure es como un límite de gasto que tú defines: "no quiero gastar más de X este mes (o este trimestre)". Cuando el gasto se acerca a ese límite (p. ej. al 80 % o al 100 %), el sistema te avisa por correo o por una acción configurada. El presupuesto no impide que sigas creando recursos ni que sigas consumiendo; solo te alerta. Sirve para supervisar el gasto y reaccionar a tiempo, no para bloquear el uso.

## Definición

Un presupuesto en Azure Cost Management es un límite de gasto configurado sobre un ámbito (suscripción, grupo de recursos o grupo de administración) con alertas que se disparan cuando el costo alcanza umbrales definidos (p. ej. 80 %, 100 %, 120 %); no bloquea la creación de recursos ni el consumo.

Permite:

- Definir un límite de gasto (presupuesto) por suscripción, grupo de recursos o grupo de administración
- Configurar alertas cuando el gasto alcanza umbrales (p. ej. 80 %, 100 %)
- Recibir notificaciones por correo o mediante Action Groups (webhook, runbook, etc.)
- Supervisar el gasto acumulado en el período del presupuesto (mensual, trimestral, anual)
- Reaccionar a tiempo ante sobrepasos; el presupuesto no detiene el uso

## Componentes

**Ámbito del presupuesto** – Nivel al que se aplica el presupuesto: suscripción, grupo de recursos o grupo de administración

**Cantidad del presupuesto** – Límite de gasto en la moneda de la suscripción (p. ej. 1000 USD/mes)

**Período del presupuesto** – Intervalo de tiempo: mensual, trimestral o anual; el presupuesto se reinicia al inicio de cada período

**Umbrales de alerta** – Porcentajes del presupuesto que disparan una alerta (p. ej. 80 %, 100 %, 120 %)

**Destinatarios de alerta** – Lista de correos o Action Group que reciben la notificación cuando se alcanza un umbral

**Action Group** – Grupo de acciones (correo, SMS, webhook, runbook de Automation) que se ejecuta cuando se dispara la alerta del presupuesto

## Funcionalidad

1. Se crea un presupuesto en Cost Management para un ámbito (suscripción, grupo de recursos o grupo de administración)
2. Se define la cantidad del presupuesto (p. ej. 5000 USD) y el período (mensual, trimestral, anual)
3. Se configuran umbrales de alerta (p. ej. 80 %, 100 %, 120 %) y destinatarios (correos o Action Group)
4. Cost Management evalúa el gasto acumulado en el ámbito respecto al presupuesto
5. Cuando el gasto alcanza un umbral configurado, se envía la alerta a los destinatarios (o se ejecuta el Action Group)
6. Se pueden crear varios presupuestos para el mismo ámbito (p. ej. uno mensual y uno trimestral)
7. El presupuesto no impide crear recursos ni consumir más; solo notifica

## Casos de Uso

- Definir un límite de gasto mensual por suscripción y recibir alerta al 80 % para revisar antes de sobrepasar
- Supervisar el gasto por grupo de recursos (p. ej. entorno de desarrollo) con presupuesto y alertas
- Configurar Action Group para enviar notificación a un canal de Teams o ejecutar un runbook cuando se alcanza el 100 %
- Crear presupuestos trimestrales o anuales por grupo de administración para planificación
- Combinar presupuestos con etiquetas y análisis de costos para asignar gasto por departamento o proyecto

## Errores Comunes

- Creer que el presupuesto bloquea el gasto o impide crear recursos (solo envía alertas; no detiene el uso)
- Pensar que las alertas se envían solas sin configurar destinatarios (hay que añadir correos o Action Group)
- Confundir el ámbito del presupuesto (suscripción, grupo de recursos, grupo de administración) con el ámbito de facturación del contrato
- Asumir que un solo presupuesto cubre todas las suscripciones (cada presupuesto tiene un ámbito; para varias suscripciones se puede usar un presupuesto a nivel de grupo de administración o uno por suscripción)
- Olvidar que el presupuesto se reinicia en cada período (mensual/trimestral/anual); no es un límite acumulado indefinido

## Preguntas

1. ¿Un presupuesto en Azure Cost Management define un límite de gasto sobre un ámbito y envía alertas cuando se alcanzan umbrales?

2. ¿El presupuesto bloquea la creación de recursos o el consumo cuando se supera el límite?

3. ¿Los presupuestos se pueden configurar para suscripción, grupo de recursos o grupo de administración?

4. ¿Para recibir notificaciones cuando se alcanza un umbral hay que configurar destinatarios (correos o Action Group)?

5. ¿Se pueden configurar varios umbrales (p. ej. 80 %, 100 %, 120 %) en un mismo presupuesto?

6. ¿El período del presupuesto (mensual, trimestral, anual) define cuándo se reinicia el cálculo del gasto acumulado?
